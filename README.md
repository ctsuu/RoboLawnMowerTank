# RoboLawnMowerTank
Autonomous, Tank track drive, Acreage, Lawn Mower, Gas Powered. 

## Scope of Work
To build a autonomous gas powered tank track drived lawn mower that aim for the large area work, such as acreage, farm and parks. 

The lawn mower based on KB750-8A model, 130KG, cutting path 550mm wide. Moving speed 0-6km/hr. Slope 0-30 deg. Remove control range 100m. Engine output 7.5 horse power.

## Assumption: 
I haven't see the real machine yet, therefore, I made some necessary assumptions in order to complete the high lever control system design. 

1. Electrical power supply. The original lawn mower may not have enough battery power to run additional electronic sensors and devices. I consider add a battery holder for a 12V 20AH AGM SLA Battery, and charger. 
2. Build the Controller enclosure, Power distribution, fuse, 12VDC-19VDC converter, waterproved connector, the Emergency stop push button and wire, operation beacon light, GPS and Wifi, on board computer and other parts as needed.
3. I assumpt the lawn mower is using generic PWM Radio Control servo, I will manage the output signal is able to drive standard RC servo. One channel for Forward/Backward, one channel for Left/Right. Pluse 5 channel digital channels, on and off for cutter up/down.  
4. I will need add necessary cameras and lidar to detect obstacle, and unexpected events. Many special designed traffic cones needed to mark the working area for safety and SLAM propose. 
5. I am going to have a stronger processing computer off the machine, to handle the initial boundary waypoint setup (Geofencing), the detailed path waypoint(0.2m-0.5m resolution) calculation, and provide base GPS location and Wifi access point. 
