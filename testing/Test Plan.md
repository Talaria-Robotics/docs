# Test Plan  
*Version 3 - 4/25/2025*

The Test Plan for the Mail Delivery Robot will include the required testing of the robot’s mechanical, electrical, and software. This plan is divided into five major tests: Electric Circuit, Mechanical System, User Interaction, Route Planning, and Autonomous Delivery. The Test Matrix document will provide the mapping of requirements to these specific tests and standard documentation, in Google Docs, of all tests will be followed.

Each test will have the following information: test name, goal of test, location of test, test parameters, and any other necessary information needed, such as limits for meeting technical requirements. The document will be submitted in soft copy.

**Test Results**  
After prototype and systems testing, the results will be verified and documented for verification that all requirements of the Mail Delivery Robot have been met. The documentation will follow the same progression as the original test plan. 

## Electric Circuits

### EC-01

***Name:*** Voltage Across Robot  
***Location:*** PIC  
***Goal of Test:*** To verify that the voltages for each component match with the expected, calculated voltages of the schematic.  
***Procedure:*** 

1. Connect all electrical components to the robot chassis and one another. Visually inspect that the connections match the schematic.  
2. Apply the battery power source and turn the robot on.  
3. Using a voltmeter, check the input voltages of:  
   1. Navigator Raspberry Pi   
   2. Control Panel Raspberry Pi    
   3. LIDAR   
   4. Touchscreen   
   5. Left Motor Driver   
   6. Left Motor  
   7. Left Encoder   
   8. Right Motor Driver   
   9. Right Motor  
   10. Right Encoder 

   ***Dates:*** 02/12/2025 \- Everything except the touchscreen \
               03/18/2025 \- Full System

   ***Results:*** 

* All components were properly wired and passed the visual inspection.  
* Input voltages to the components matched the desired outcome from the electric schematic.  
* Touchscreen was tested on 03/18/2025.  
* Original battery source failed on 03/26/2025 and a new one was ordered. We received the new battery on 3/31/2025.

### EC-02

***Name:*** Battery Life  
***Location:*** PIC  
***Goal of Test:*** To verify the lifetime of the battery of the robot to have at least one hour operation.  
***Procedure:*** 

1. Take the battery off of the charger and record the battery’s percentage, which should be at 95% or higher.  
2. Connect the battery and turn on the robot. Record the starting time.  
3. Run the robot at full power to all systems. Moving the robot around the workspace.   
4. After at least an hour, turn off the robot and record the ending time.  
5. Replace the battery in the charging station and record the battery’s percentage.  
     
   ***Date:*** 3/22/2025  
   ***Results:***   
* Conducted this test in parallel with Test MS-03.  
* Battery started at 4 bars \~ 80%  
* After an hour, the battery was still at 4 bars \~ 80%


### EC-03

***Name:*** Raspberry Pi Connections  
***Location:*** PIC  
***Goal of Test:*** To verify the connections between the Raspberry Pis, that they are able to communicate with one another.  
***Procedure:*** 

1. Connect the Raspberry Pis with the power source and together with an ethernet cable.  
2. Conduct visual inspection that all components are properly wired.  
3. Send a text message from the Navigator Pi to the Control Panel Pi. Record if the message is successfully received.  
4. Send a LIDAR map from the Navigator Pi to the Control Panel Pi. Record if the message is successfully received.  
5. Send a completed delivery message from the Control Panel Pi to the Navigator Pi. Record if the message is successfully received.

   ***Date:*** 3/19/2025

   ***Results:*** 

* Raspberry Pis were connected and all components passed the visual inspection test.  
* A message was successfully sent through the Navigator Pi and successfully received from the Control Panel Pi  
* The LIDAR map was also successfully communicated between the two Raspberry Pis.  
* Navigator Pi and Control Panel can also successfully communicate delivery messages.

### EC-04

***Name:*** Touchscreen and LIDAR Active  
***Location:*** PIC  
***Goal of Test:*** To verify that the touchscreen and LIDAR are in working condition.  
***Procedure:*** 

1. Connect the power source to the touchscreen and LIDAR.  
2. Conduct a visual inspection that all components are properly wired. The Control Panel Raspberry Pi will be connected to the touchscreen and the Navigator Raspberry Pi will be connected to the LIDAR.  
3. Turn on the touchscreen and send a short interactive program. Ensure that the touchscreen is reactive to touch.  
4. Send LIDAR readings to a laptop and graph its vision. Ensure that it is reactive to objects moving in front of it. 

   ***Dates:*** 02/25/2025 for LIDAR \
               03/17/2025 for Both LIDAR and Touchscreen

   ***Results:*** 

* LIDAR is able to detect objects. We used a NodeRED GUI to visualize the LIDAR’s data while moving objects in front of it and comparing our physical motion with the visualization.  
* The touchscreen is interactive and can process a series of buttons being pressed.  
* Both the Navigator and Control Panel Raspberry Pis can communicate with one another.

### EC-05

***Name:*** Raspberry Pi Controlling Motors  
***Location:*** PIC  
***Goal of Test:*** To verify that the Raspberry Pis are able to communicate with motors.  
***Procedure:*** 

1. Conduct visual inspection that the motors, encoders, power supply, and Navigator Raspberry Pi are connected.  
2. Send a signal through the Navigator to the motors to move forward for 10 seconds.  
3. Rotate the motors backwards for 10 seconds.  
4. Rotate the left motor forwards and the right motor backwards for 10 seconds.  
5. Rotate the left motor backwards and the right motor forwards for 10 seconds.

   ***Date:*** 02/24/2025

   ***Results:*** 

* Completed visual inspection and the robot was properly wired.  
* Robot motors were successfully able to rotate forward, backwards, and in opposite directions for turning left and right.  
  


## Mechanical System

### MS-01

***Name:*** Robot Chassis Motion  
***Location:*** Fermier Hall or PIC  
***Goal of Test:*** Test robot’s range of motion and ability to move around the workspace.  
***Procedure:*** 

1. Turn on the robot. Record time and current battery percentage from its charging station. Visual inspection that all components are active and functional.  
2. Move the robot forward 1 m with \+/- 2 cm deviation on tile.   
3. Move the robot backwards 1 m with \+/- 2 cm deviation on tile.  
4. Turn the robot a minimum of clockwise 360॰ on tile.  
5. Turn the robot a minimum of  counterclockwise 360॰ on tile.  
6. Repeat steps 2-5 on carpet.  
7. Move the robot across the joint between the two floor types. Once from carpet to tile and once from tile to carpet.  
8. Turn off the robot. Record time and current battery percentage from its charging station.

   ***Date:*** 4/8/2025

   ***Results:*** 

* Robot passed visual inspection   
* We adjusted to moving 2 ft forward and backwards. The robot was able to do both with a margin of error with less than a half inch.  
* The robot was also able to rotate 360॰ in both directions.  
* The robot’s initial battery was at 4 bars \~= 80% and it ended on 3 bars \~= 60%. (Several attempts were made to complete this test, resulting in the loss of battery power).  
* We have yet to test its ability on carpet and on the transition between floor types.

### MS-02

***Name:*** Robot Chassis Motion with Distances  
***Location:*** Fermier Hall or PIC  
***Goal of Test:*** Test robot’s range of motion and ability to move around the workspace.  
***Procedure:*** 

1. Turn on the robot. Record time and current battery percentage from its charging station. Visual inspection that all components are active and functional.  
2. Move the robot forward 1 m with \+/- 0.657 cm deviation on tile. Record distance.  
3. Move the robot forward 12.192 m with \+/- 8 cm deviation on tile. Record distance.  
4. Turn off the robot. Record time and current battery percentage from its charging station.  
     
   ***Date:*** 4/10/2025  
   ***Results:***   
* Robot passed visual inspection and the initial battery was at 4 bars \~= 80%.  
* We adjusted the distances to 2 ft and 25 ft.  
* Robot was able to move 2 ft with a deviation of half an inch.  
* Robot was able to move 25 ft with a deviation of 15 inches.  
* The battery was at 4 bars \~= 80% at the end of the test.

### MS-03

***Name:*** Robot Chassis Motion with Weight  
***Location:*** Fermier Hall  
***Goal of Test:*** Test robot’s range of motion, ability to move around the workspace, and carry up to 15 lbs of weight.  
***Procedure:*** 

1. Turn on the robot. Record time and current battery percentage from its charging station.   
2. Move the robot forward 1 m with \+/- 0.657 cm deviation on tile and on carpet.  
3. Add 5 lbs of weight into the robot’s mail storage and move the robot forward 1 m with \+/- 0.657 cm deviation on tile and on carpet. Record distance for accuracy.  
4. Repeat step 3 with 10 lbs and 11, 12, 13, 14, and 15 lbs of weight. Record distances.  
5. Turn off the robot. Record time and current battery percentage from its charging station.  
     
   ***Date:*** 3/22/2025  
   ***Results:***   
* Testing Weights:  
  1. Small Weight \= 3 lbs 3 oz \= 3.1875 lbs  
  2. Large Weight \= 4 lbs 8 oz \= 4.5 lbs  
  3. Water Bottle 1 \= 2 lbs 5 oz \= 2.3125 lbs  
  4. Water Bottle 2 \= 2 lbs 5 oz \= 2.3125 lbs  
  5. Wheel 1 \= 1 lb 15 oz \= 1.9375  
  6. Wheel 2 \= 1 lb 15 oz \= 1.9375  
* Starting Time: 9:00pm, Ending Time:  9:15pm  
* Starting Battery: 4 bars (\>80%) , Ending Battery: 4 bars (\~80%)   
* Tests:  
1. Total Weight \= 3.1875 lbs (Small Weight)  
   1. Completed, moved 2 ft  
2. Total Weight \= 7.6875 lbs (Small and Large Weight)  
   1. Completed, moved 2 ft  
3. Total Weight \= 10.000 lbs (Small and Large Weights and Water Bottle 1\)  
   1. Completed, moved 2 ft  
4. Total Weight \= 11.9375 lbs (Small and Large Weights and Water Bottles 1 and 2\)  
   1.  Completed, moved 2 ft  
5. Total Weight \= 13.8750 lbs (Small and Large Weights and Water Bottles 1 and 2, and Wheel 1\)  
   1. Completed, moved 2 ft  
6. Total Weight \= 16.1875 lbs (Small and Large Weights and Water Bottles 1 and 2, and Wheels 1 and 2\)  
   1. Completed, moved 2 ft  
* There is slight bowing on the front idler wheels, but the robot is functional under the weight  
* The bowing was fixed on 4/13/2025

### MS-04

***Name:*** Robot Chassis Motion with Weight Stabilization  
***Location:*** PIC  
***Goal of Test:*** Test robot’s range of motion and ability to move around the workspace.  
***Procedure:*** 

1. Turn on the robot. Record time and current battery percentage from its charging station.  
2. With 5 lbs of weight loaded onto the robot, move the robot in a 1x1 m square, at a speed of 0.25m/s. Ensure that the weight does not fall off or out of the robot, make notes on stability.  
3. Repeat step 2 with 10 lbs and 15 lbs of weight.  
4. Move the robot across the joint between the two floor types. Once from carpet to tile and once from tile to carpet.  
5. Turn off the robot. Record time and current battery percentage from its charging station.  
     
   ***Date:*** 3/22/2025  
   ***Results:***   
* Robot’s battery was at 4 bars \~= 80% and after testing it was still at 4 bars \~= 80%  
* We only tested on tile  
* Robot was successful in completing the motion with 16.1875 lbs.

## User Interaction

### UI-01

***Name:*** Touchscreen Interaction  
***Location:*** PIC  
***Goal of Test:*** Test touchscreen’s ability to program a route through user input.  
***Procedure:*** 

1. Conduct visual inspection of the robot and ensure all connections are secure.  
2. Flash the touchscreen with the Mail Delivery System GUI.  
3. Follow the prompts on the touchscreen to create a route plan. Record reaction time between touchscreen interaction and progression to the next page.

   ***Date:*** 3/18/2025

   ***Results:*** 

* Robot passed a visual inspection.  
* The touchscreen was able to be flashed with the GUI and was responsive to user interaction and touch. Response time was less than 1 second.

### UI-02

***Name:*** Touchscreen and Chassis Communication  
***Location:*** Fermier  
***Goal of Test:*** Test robot’s ability to communicate between a user’s programmed route and starting chassis motion.  
***Procedure:*** 

1. Conduct visual inspection of the robot and ensure all connections are secure.  
2. Flash the touchscreen with the Mail Delivery System GUI.  
3. Follow the prompts on the touchscreen to create a route plan..  
4. Initiate motion through the GUI’s “Start” function. Record reaction time from touchscreen interaction and movement of the motors.  
5. Allow the robot to move through the user's programmed route, without obstacles.  
6. Ensure that once the robot reaches a stop, the touchscreen prompts the next user to “accept” the delivery and instruct the robot to continue on its path. Record accuracy of the robot’s path by comparing predicted and actual positions, measured distances, and delays.

   ***Date:*** 4/24/2025

   ***Results:*** 

* Robot passed a visual inspection.  
* Robot was able to direct the user through the path planning process.  
* The UI was able to communicate with the Navigator to initiate motion.  
* The route consisted of two separate rooms. The robot was able to successfully navigate to these rooms and back home. It would deviate from the final home position by 1 ft.

## Route Planning

### RP-01

***Name:*** Static Obstacle Detection and Avoidance  
***Location:*** Fermier  
***Goal of Test:*** Test the robot’s ability to detect static obstacles, avoid them, and continue on its path.  
***Procedure:*** 

1. Conduct visual inspection of the robot and ensure all connections are secure.  
2. Connect the laptop to the Navigator Raspberry Pi and LIDAR.  
3. Record current findings from the LIDAR, then add a static object in front of the LIDAR. Record changes.  
4. Program the robot to move forward for 6 ft and place a static object in its path. Record starting position. Use painter’s tape on the floor to visualize the anticipated path.  
5. Run the new robot program. Ensure that the robot stops within 6 inches of the static object.   
     
   ***Date:*** 4/24/2025  
   ***Results:***   
* The robot passed the visual inspection.  
* The lidar was accurately able to detect static obstacles and was successfully able to stop within 6 inches of an obstacle.

### RP-02

***Name:*** Static Obstacle Detection and Avoidance on Path with Turn  
***Location:*** Fermier  
***Goal of Test:*** Test the robot’s ability to turn, detect static obstacles, avoid them, and continue on its path.  
***Procedure:*** 

1. Conduct visual inspection of the robot and ensure all connections are secure.  
2. Connect the laptop to the Raspberry Pi and LIDAR.  
3. Record current findings from the LIDAR.  
4. Program the robot to move forward for 3 feet, turn clockwise 90°, and move forward 3 feet. Place a static object at the turning point and use painter’s tape on the floor to visualize the anticipated path.  
5. Record the robot’s current position and run the new robot program:  
   1. Ensure that the robot stops within 6 inches of the static obstacle and waits for 10 seconds.  
   2. Check that the robot moves around the static obstacle and returns back to the anticipated path. Record if successful, if it deviates from the path, and how much it deviates from the path.  
6. Record the robot’s end position and if there is any deviation from the anticipated end position.

   ***Date:*** 4/24/2025

   ***Results:*** 

* The robot passed the visual inspection.  
* The robot was able to move the desired path of 3 feet, clockwise rotation of 90°, and move forward again 3 feet.  
* The lidar was accurately able to detect static obstacles and was successfully able to stop within 6 inches of an obstacle.  
* The robot was unable to move around the static obstacle, rather, changes were made to treat static and dynamic obstacles similarly, to not deviate from the path.

### RP-03

***Name:*** Dynamic Obstacle Detection and Avoidance  
***Location:*** PIC  
***Goal of Test:*** Test the robot’s ability to detect dynamic obstacles, avoid them, and continue on its path.  
***Procedure:*** 

1. Conduct visual inspection of the robot and ensure all connections are secure.  
2. Connect the laptop to the Raspberry Pi and LIDAR.  
3. Record current findings from the LIDAR, then move a dynamic object in front of the LIDAR. Record changes.  
4. Program the robot to move forward for 6 feet and have a dynamic object ready to move in front of it during the path. Use painter’s tape on the floor to visualize the anticipated path.  
5. Run the new robot program and move the dynamic object in front of it. Ensure that the robot stops within 6 inches of the dynamic object and waits for 10 seconds to allow the object to pass by.   
6. Ensure that the robot stays on the anticipated path and completes its program. Record the ending position and any deviation from the path.

   ***Date:*** 04/24/2025

   ***Results:*** 

* The robot passed the visual inspection.  
* The robot was able to move the desired path of 37 feet, with only a deviation of 15 inches horizontally from its desired ending position.   
* The lidar was accurately able to detect dynamic obstacles and was successfully able to stop within 6 inches of an obstacle.


### RP-04

***Name:*** Static and Dynamic Obstacle Detection and Avoidance on Straight Path  
***Location:*** PIC  
***Goal of Test:*** Test the robot’s ability to detect static and dynamic obstacles, avoid them, and continue on its path.  
***Procedure:*** 

1. Conduct visual inspection of the robot and ensure all connections are secure.  
2. Connect the laptop to the Raspberry Pi and LIDAR.  
3. Record current findings from the LIDAR.  
4. Program the robot to move forward for 10 ft. Have a static object, on the first half of the path, and prepare a dynamic object, on the second half of the path, to move in front of the robot during its path. Use painter’s tape on the floor to visualize the anticipated path.  
5. Record the robot’s current position and run the new robot program:  
   1. Ensure that the robot stops within 6 inches of both the static and dynamic obstacles and waits for 10 seconds.  
   2. Check that the robot moves around the static obstacle and returns back to the anticipated path. Record if successful, if it deviates from the path, and how much it deviates from the path.  
   3. Check that the robot waits for the dynamic obstacle to pass and continues on its path. Record if successful.  
6. Record the robot’s end position and if there is any deviation from the anticipated end position.  
7. Repeat steps 9-12 with a dynamic obstacle on the first half of the path and a static obstacle on the second half of the path. 

   ***Date:*** 04/24/2025

   ***Results:*** 

* The robot passed the visual inspection.  
* The robot was able to move the desired path of 10 feet, accurately.  
* The lidar was accurately able to detect static obstacles and was successfully able to stop within 6 inches of an obstacle.  
* The robot was unable to move around the static obstacle, rather, changes were made to treat static and dynamic obstacles similarly, to not deviate from the path.

## Autonomous Delivery

### AD-01

***Name:*** User Programs Robot and Robot Follows Path  
***Location:*** PIC  
***Goal of Test:*** Test the robot’s ability to accept user input to program the route and move to follow the route.  
***Procedure:*** 

1. Conduct visual inspection of the robot and ensure all connections are secure.  
2. Program the robot through the touchscreen for one stop. Record starting position. Use painter’s tape on the floor to visualize the anticipated path.  
3. Run the new robot program. Record the final position and any deviations from the path. Ensure that when the robot reaches its final location, the touchscreen prompts user interaction to “accept mail.”  
4. Repeat steps 2 and 3 with programming the same path and including obstacles. In each scenario, ensure that the robot stops within 6 inches of the object, waits 10 seconds, makes the appropriate action based on its obstacle type, and continues its path. The following tasks are:  
   1. Add a static obstacle in the path.   
   2. Add a dynamic obstacle in the path.  
   3. Add a static and dynamic obstacle in the path. 

   

   ***Date:*** 04/24/2025

   ***Results:*** 

* Robot passed the visual inspection test and all connections were secure.  
* The robot was able to locate the positions of all rooms, with deviances ranging from 2 inches to 6 inches. The main cause of error was the turning, as it was not pivoting from the same central location each time.  
* The robot was unable to move around the static obstacle, rather, changes were made to treat static and dynamic obstacles similarly, to not deviate from the path. The robot was able to stop within 6 inches for both dynamic and static obstacles. 


### AD-02

***Name:*** Full Route in Sections  
***Location:*** PIC  
***Goal of Test:*** Test the robot’s ability to autonomously travel and avoid obstacles between all programmable points.  
***Procedure:*** 

1. Conduct visual inspection of the robot and ensure all connections are secure.  
2. Program the robot through the touchscreen for one stop: Mail Room to Room \#1. Record starting position. Use painter’s tape on the floor to visualize the anticipated path.  
3. Run the new robot program. Record the final position and any deviations from the path. Ensure that when the robot reaches its final location, the touch screen prompts the user to click “accept mail.”  
4. Re-run the route with a static and dynamic obstacle along the path.  
5. Repeat steps 2, 3, and 4 with the following routes:  
   1. Mail Room to Room \#2  
   2. Room \#1 to Room \#2  
   3. Room \#2 to Room \#1  
   4. Room \#1 to Mail Room  
   5. Room \#2 to Mail Room

   ***Date:*** 04/24/2025

   ***Results:*** 

* Robot passed the visual inspection test and all connections were secure.  
* The robot was able to locate the positions of all rooms, with deviances ranging from 2 inches to 6 inches. The main cause of error was the turning, as it was not pivoting from the same central location each time.  
* The robot was able to move between all segments.  
* The UI was able to initiate motion of the robot and the correct prompts were demonstrated.


### AD-03

***Name:*** Full Autonomous Route  
***Location:*** Fermier  
***Goal of Test:*** Test the robot’s ability to autonomously travel and avoid all obstacles in a complete delivery path.  
***Procedure:*** 

1. Conduct visual inspection of the robot and ensure all connections are secure.  
2. Program the robot through the touchscreen for one stop: Mail Room to Room \#1. Record starting position. Use painter’s tape on the floor to visualize the anticipated path.  
3. Run the new robot program. Record the final position and any deviations from the path. Ensure that when the robot reaches its stop, the touch screen prompts the user to interact to “accept mail,” and the robot continues to its next location.  
4. Re-run the route with a static and dynamic obstacle along the path.  
5. Repeat steps 2, 3, and 4 with the following routes:  
   1. Mail Room, Room \#1, and Mail Room  
   2. Mail Room, Room \#2, and Mail Room  
   3. Mail Room, Room \#1, Room \#2, and Mail Room  
   4. Mail Room, Room \#2, Room \#1, and Mail Room

   ***Date:*** 04/24/2025

   ***Results:*** 

* Robot passed the visual inspection test and all connections were secure.  
* The robot was able to locate the positions of all rooms, with deviances ranging from 2 inches to 6 inches. The main cause of error was the turning, as it was not pivoting from the same central location each time.  
* The robot was able to move between all segments and complete all potential routes  
* The UI was able to initiate motion of the robot and the correct prompts were demonstrated.
