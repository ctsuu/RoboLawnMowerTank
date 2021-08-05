# RoboLawnMowerTank
Autonomous, Tank track drive, Acreage, Lawn Mower, Gas Powered. 

## Scope of Work
To build a autonomous gas powered tank track drived lawn mower that aim for the large area work, such as acreage, farm and parks. 

The lawn mower based on KB750-8A model, 130KG, cutting path 550mm wide. Moving speed 0-6km/hr. Slope 0-30 deg. Remove control range 100m. Engine output 7.5 horse power.

## Assumption: 
I haven't see the real machine yet, therefore, I made some necessary assumptions in order to complete the high lever control system design. 

1. Electrical power supply. The original lawn mower may not have enough battery power to run additional electronic sensors and devices. I consider add a battery holder for a Dewalt DCB 609-2 20V/60V 9.0Ah Battery, and charger. 
2. Build the Controller enclosure, Power distribution, fuse, DC-DC converter, waterproof connectors, the Emergency stop push button and wire, operation beacon light, GPS and Wifi, on board computer and other parts as needed.
3. I assume the lawn mower is using generic PWM Radio Control servo, I will manage the output signal is able to drive standard RC servo. One channel for Forward/Backward, one channel for Left/Right. Plus 5 channel digital channels, on and off for cutter up/down.  
4. I am going to use cameras and lidar to detect obstacle, and unexpected events. Many special designed traffic cones needed to mark the working area for safety and SLAM propose. 
5. I am going to have a hign spec processing computer off the machine, to handle the initial boundary waypoint setup (Geofencing), the detailed path waypoint(0.2m-0.5m resolution) calculation, and provide base GPS location and Wifi access point. This computer may handle more than one robot in the same area. The computer is mounted on the service truck, the service truck hauls all robots to the working zone, fuel the robots, and charging batterise as needed. 

## Hign Level Design Concept: 
Following each assumptions, I calculated requirments and souring the parts for this project. 
1. Given power budget 24V 4A total power consumption for the onboard computer and sensors, a 20V 9AH hour battery can provide 1 hour of run time.

2. 300mmx400mmx170mm waterproof box is suitable for the controller enclosure. See details of all components in the cost estimate. 

3. The Jetson Nano Developer Kit 4G version may have enough power to handle sensor data colletion, and motion control functions. Using usb - servo adapter to provide the PWM signals. 2 channels at this point. Necessary HAT or termial blocks will added to the system. 

4. Print and cutout 50 unique designed visual land mark traffic cones.
Using Waterproof Network camera for visual detection, everything other than grass will raise alarm. 
Using Livox Lidar for distance detection, provide warming zone, slow down zone and stop zone detection. Maximun 27m detection range. 
Build SLAM function to improve location accuracy to sub meter level. Allow the cutting path overlap together. 

5. Central controller: One to many robots in mind. Doing one to one control at this point. Manually setup the geofencing, the outside perameters and inside islands, placing the traffic cones, generate the detailed cutting path and send to the robot. Robot should run on their own and supervised by the central controller. Controller can disable the robot, or take over the control via Wifi link.  

6. Machine operation safety is the first priority to ensuring the all possible protective measures have been taken to prevent injury to workers in and around the automated machine. It also protecting the machine from misuse by the operator. My design concept is referenced to standards ISO 13849-1 and IEC 61508. Hard wired relay control panel are used for safety control. Controllers with redundancy of design and fault detection. Networks with fault checking and diagnostics. 

## Risk Assessment and Reduction
We will host a section to determining hazards in the machine control system and level of hazards.The documentation of process us maintained. Machine operators, maintenance personnel and management will be involved. Everyone's point of view should be evaluated. The following guidlines are used:

1. Defines the limitations of the machine: Intended use, foreseeable misuse, expected training and experience, possible exposure to machine hazards.

2. Defines hazardous conditions: Mechanical hazards(Severing, entanglement, crushing, vibration), Thermal hazards(Burns), Environmental hazards(Sound, chemical, radiation)

3. Risk factors are determined and risk estimated: Degree of harm and Porbability

4. Risk Evaluation: Determine if risk must be reduced.

5. Take Safety measures according to ISO 12100: Remove dangers, reduce exposure frequency, maintain visibility, add guarding, employ redundant systems with fault checking.

6. Repeat the entire process until all risk are within acceptiable level. 

The control system is designed to meet ISO 13849-1 Category 3. - Single fault does not lead to loss of safety function. Fault shall be detected at or before next demand. The safety component has MTTFd (Mean Time to Dangerous Failure) of 20 years(Medium). It also has DCavg (Average Diagnostic Coverage) at 95% (Medium), Therefore, overall system performance level is PLd. 

Based on the risk scores, This machine have to meet IEC 61508 SIL 3, the safety component have to meet PFH (Probability of failure per hour) >=10^-8  to < 10^07. 
