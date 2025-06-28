# Functional Specification 
*Version 3 - 03/18/2025*

1. **Design**  
   1. Maximum dimensions  
      1. Max package size of 15” x 11” x 10” (L x W x H)  
      2. All folders will be letter size, 9” x 11”, or smaller  
      3. Combined weight of packages and folders will not exceed 15 pounds  
   2. Mail will be secured  
      1. Mail does not fall out during programmed motion  
   3. Clean and organized design  
      1. All cables will be secured  
   4. Robot volume will not exceed 24” x 28” x 24” (L x W x H)  
   5. Driving method   
      1. Robot will have enough traction to avoid slipping on tile and carpet  
      2. Tank treads are preferred  
   6. Motors  
      1. A minimum of two motors  
      2. Motors will be controlled by a motor driver  
      3. Motors will be related to encoders for closed loop velocity control  
2. **Set Up**  
   1. Robot will be placed in the same marked position on every run  
      1. User can place masking tape can be to record the position  
      2. User can start the robot touching a designated wall  
   2. User will ensure that the system is adequately charged, as defined by the percentage on the battery charger, prior to starting  
      1. Batteries should be above 20%  
   3. Robot will travel a maximum of 3 stops, not including the mail room  
   4. Normal Operation  
      1. User will load robot with mail before selecting the desired rooms  
      2. Robot will navigate to desired location while avoiding obstacles  
      3. Robot must wait for end user to instruct it before continuing its path  
3. **Autonomous Navigation**  
   1. Indoor navigation only  
      1. Testing will occur on the first floor of Fermier Hall and in the PIC  
   2. Mapping  
      1. Map will be preloaded  
      2. Route will be programmable  
      3. The user will have the ability to select any combination of the listed rooms  
   3. Obstacle Avoidance  
      1. Robot will avoid static and dynamic obstacles  
         1. Robot will stop if an object is within 6”  
         2. Robot will attempt to navigate around an object if it is more than 6” away  
      2. Obstacle avoidance sensor will not be a physical detection method (e.g. whiskers or bumpers)  
         1. LiDAR is preferred  
   4. Speed  
      1. Motors will not exceed 1 m/s under no load  
      2. Motors will be able to run at 0.25 m/s under the maximum mail load

      

      

4. **Touchscreen**  
   1. Touchscreen will be visible at all times   
   2. Touchscreen will be larger than 5”  
   3. Touchscreen is reactive when touched  
5. **Power**  
   1. Power supply will be supplied using portable batteries  
      1. Batteries used for any module in the system must meet the following criteria:  
         1. Sufficiently power all components  
         2. Provide one hour of non-continuous operation per day   
   2. Batteries must be removable and chargeable in a separate wall-station  
6. **Communication**  
   1. Raspberry Pis will be connected using Ethernet or another stable form of communication  
   2. Robot will not communicate with any technology not attached to the mobile system
