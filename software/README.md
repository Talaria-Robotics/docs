Talaria's autonomous mail delivery robot is built in two halves: the Navigator and Control Panel. The Navigator module is composed of a Raspberry Pi, the motor controller, and all navigation sensors such as LIDAR and motor encoders. Its primary purpose is to accept control commands from the Control Panel and navigate the SCUTTLE on the delivery route. The Control Panel module consists of another Raspberry Pi and a touchscreen, which serves as the interface for users to interact with the delivery system, primarily by planning and accepting deliveries.

**In short:**

* The [Navigator](#navigator) is the brains of the SCUTTLE platform including all navigation sensors
    * The Navigator [API](#api) is the surface used for high-level navigation commands
    * The Navigator Controller is the control loop that uses sensors and motors to move between waypoints
* The [Control Panel](#control-panel) is the primary interface between the user and the robot

***Figure 1:** High-level sequence of system events.*
![](./user-flow.png)

***Figure 2:** Communication sequence for the delivery system.*
![](./system-sequence.png)

# Navigator

* Receives commands from [Control Panel](#control-panel)
* Stores floor map, rooms, and available bins
* Determines most efficient order of stops
* Plans ideal driving route
* Controls motors while avoiding obstacles using feedback from LIDAR and encoders

## API
The Navigator API acts as a layer between the [Control Panel](#control-panel) and the robot control loop. The interface itself is agnostic of any particular protocol, but for Talaria PRESTON it is implemented using HTTP via an Ethernet cable between the two Raspberry Pis (see [*Implementation*](#implementation)). In Dart, the interface looks like this:

```dart
abstract interface class NavigatorApi {
  Future<PossibleMailRouteInfo> getPossibleRouteInfo();

  Future<void> setRoute(RequestedMailRoute route);

  Stream<MailRouteEvent> listenToRoute();

  Future<void> deliveryCompleted();
}
```

### Route info
`getPossibleRouteInfo()` returns a structure that includes the available rooms and bins:

```json
{
  "id": "someGUID",
  "name": "Example Floor",
  "rooms": [
    {
      "id": "home",
      "name": "Mail Room"
    },
    {
      "id": "room1",
      "name": "Room 101"
    },
    {
      "id": "room2",
      "name": "Room 102"
    },
  ],
  "bins": [
    {
      "number": 1,
      "name": "Letter Slot 1"
    },
    {
      "number": 2,
      "name": "Letter Slot 2"
    },
    {
      "number": 5,
      "name": "Package Areas"
    },
  ]
}
```

### Route events
`listenToRoute()` streams a sequence of events from the Navigator of any of the following formats. Every event type has two properties: `$type` and `orderNumber`. The type property contains the name of the event type and is required so the client and deserialize the data into the proper structure. The `orderNumber` is an optional property that may be used by the client to process events correctly if they arrive out of order.

**In-transit:** The robot is on its way to the specified room.
```json
{
  "$type": "InTransit",
  "orderNumber": 1,
  "room": {
    "id": "room1",
    "name": "Room 1"
  }
}
```

**Arrived at stop:** The robot is currently waiting at the stop for the recipient to remove their mail from the specified bin.
```json
{
  "$type": "ArrivedAtStop",
  "orderNumber": 2,
  "room": {
    "id": "room1",
    "name": "Room 1"
  },
  "bin": {
    "number": 2,
    "name": "Letter Slot 1"
  }
}
```

**Return home:** The robot is currently waiting at the stop for the recipient to remove their mail from the specified bin.
```json
{
  "orderNumber": 3,
  "$type": "ReturnHome"
}
```


## Floor maps
Floor maps define the layout of a mail floor, which is used for path planning and some static obstacle avoidance. They are stored in a custom file format that encodes paths between points of delivery, referred to as stops.

Below is an example of a floor map:
```ini
[Meta]
Small Test A
77411ACA-B73D-4B02-AB38-4433573A5522

[Rooms]
mail: Mail Room
room1: Room 1
room2: Room 2
room3: Room 3

[Nodes]
mail: 2, 3
j1: 7, 5
room1: 4, 6
j2: 7, 6
room2: 7, 8
room3: 10.5, 3

[Paths]
mail > j1: H 7
j1 > room1: H 4
j1 > j2:
j2 > room2:
j2 > room3: H 10.5
mail > room3: c 4,-2 8.530415,-3e-7 8.530415,-3e-7
```

The format is composed of four sections:

* `Meta`: Floor plan name and unique ID
* `Rooms`: All available rooms on this floor, where the first room is assumed to be Home
* `Nodes`: Defines all rooms and junctions
* `Paths`: Defines connections between nodes

The `Rooms` section is used to specify which nodes are rooms by assigning a name to each room. This, along with the floor plan metadata, is the only data provided to the Control Panel (via `GET /possibleRoute`).

The `Nodes` and `Paths` sections together define a bi-directional graph that represents the navigatable paths between points of interest.

Nodes can either be rooms, as previously described, or as junctions that serve as intermediates between rooms. Junctions allow the path planning algorithm to skip over branches in the graph that connect only to rooms the robot does not need to stop at.

In the floor map file, a node is defined with an ID, followed by a colon, followed by the global coordinates of the node: `$nodeId: $x, $y`. These coordinates are intended to be in units of centimeters to reduce conversions, but in theory they can be specified in any length unit and converted at runtime.

Paths are defined by the starting node ID, a right angle bracket, the ending node ID, a colon, and an SVG path fragment: `$startNodeId > $endNodeId: $pathFragment`. The [SVG path format](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths) was selected for its efficiency and existing tooling. A full SVG path is generated by prepending a move command with the starting node coordinates and appending a line command with the ending node coordinates: `M ${startNode.X} ${startNode.Y} $pathFragment L ${endNode.X} ${startNode.Y}`. This minimizes repetition of the node coordinates and allows simple, linear connections between nodes to be stored as empty strings. For example, `j1 > j2: ` results in a vertical line connection between `j1` and `j2` that is automatically corrected if the `j1` or `j2` nodes are moved.

***Figure 3:** Visualization of the graph defined in the example floor plan. Stops are shown in green and junctions in red.*
![](example-floorplan-graph.png)

# Control Panel
* Sends commands to [Navigator](#navigator)
* Asks delivery person to specify which bins contain mail for which rooms
* Shows a status message when bot is in transit
* Allows recipients to tell the bot when they have finished retrieving their items

In general, the Control Panel is designed to be very simple. The [Navigator API](#api) is designed in such a way that the Control Panel needs almost no domain logic or state management. Any information it needs can be immediately retrieved from the API. For example, the [in-transit event](#route-events) includes a complete room object, rather than providing only the room ID and leaving it up to the Control Panel to resolve the ID to a name. 

## UI flow
The Control Panel has four different screens that roughly correspond with the major events shown in *Figure 2*.

1. **Home:** Landing page for when the bot first starts up.
1. **Route planner:** Allows the sender to assign rooms to bins using data fetched via `getPossibleRouteInfo()`.
1. **Route confirmation:** Prompts the sender to confirm the bin-room assignments.
1. **Status:** Displays the current status of the delivery by streaming events from `listenToRoute()`.

**In-transit:** Informs passersby that the robot is on its way to a room.

![An example of the in-transit screen.](status-intransit.png)

**Arrived at stop:** Informs the recipient which bins contain mail for them. Waits for confirmation before calling `deliveryComplete()`.

![An example of the arrived-at-stop screen.](status-arrivedatstop.png)

**Return home:** Informs passersby that the robot has completed its route and is returning to its home position.

![An example of the return-home screen.](status-returnhome.png)