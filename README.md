# RoboLawnMowerTank
Autonomous, Tank track drive, Acreage, Lawn Mower, Gas Powered. 

## Scope of Work
To build a autonomous gas powered tank track drived lawn mower that aim for the large area work, such as acreage, farm and parks. 

The lawn mower based on KB750-8A model, 130KG, cutting path 550mm wide. Moving speed 0-6km/hr. Slope 0-30 deg. Remove control range 100m. Engine output 7.5 horse power.

The capabilities of this robot can be categorized as: (a) Navigation, (b) HMI (Human Machine Interface) and (c) Physical interation or Manipulation.

Navigation involves moving around in space without running into static or dynamatic obstacles such as trees and humans. HMI involves the communication between robot and controller, help the operator to understand the robot position. Finally, physical interaction or manipulation involves the ability to delivery the payload, such as mowing, moving or other tasks.

There are some key technologies we are going to explore and implement are list as following:
1. Active Agent
2. Simplify perception problems
3. Minimalist design of autonomous behaviours
4. Hardware and Software Co-design

Navigation, specifically tailored towards Outdoor Unmanned Gound Vehicels could be simplified into 2D space. However, the elevation and slope change is considered, but the robot is always remain on the ground. The fundamental questions are: Where are I? and What is the hazard when I am moving? and Where should I go next? 

We define the robot as an active agent. Compare to living agents such as birds, bees and dogs, the living beings have been solving these problems with relative ease and extreme efficiency. My concepte is to building specific task driven sensor-motor loops cell(combination of perception, planning and control). Each cell is a completed closed loop motion control system, with perception feedbacks. The cell will solve the task in local frame. The complicated task can utilize multiple of such sensor-motor loops.

The most common approach of UGV(unmanned Ground Vechicle) is based on the sensing the world in 3D. This philosopy revolves around obtaining a 3D map first and then utilizing for various tasks. However, a lot of tasks rarely require a full 3D map of the scene to be accomplished. Also the system is not minimalist. On the contrary, my tailored solution adaptes the design philosophy based on the current operating constraints of computation, sensing and power budget. The result will not directly transferable to different agent morphologies, but it is generally more power-efficient for the set of tasks it is designed for. 

The complicated real world task will be break down to agent's competence groups(also called behaviours) for eaier design and training the nerual-network. 

### Minimalist design of autonomous UGV behaviours.
Competence Passive Approach Active and Task-based Approach
Kinetic stabilization: Optimization of optical flow fields  vs. Sensor fusion between optical flow and IMU measurements
Obstacle avoidance: Obtain 3D model and plan accordingly vs. Obtain flow fields and extract relevant information from them
Segmentation of independently moving objects: Optimization of flow fields vs. Fixation and tracking allows detection
Homing: Application of SLAM vs. Learn paths to home from many locations
Pursuit and Avoidance: Reconstruct 3D model and plan accordingly vs. Track while in motion
Integration: Switching between behaviors Easy: The planner interacts with the 3D model vs. Hard: An attention mechanism on ideas switching between behaviors

### Forms of Activeness on a UGV 
Activeness on a UGV or any robot in general can be accomplished in multiple ways.
1. By moving the agent itself, 2. By employing an active sensor, 3. By moving a part of
the agent’s body, 4. By hallucinating active movements.

The first approach, the entier agent moves such that the perception problem become simpler. Such an approach is generally used by smaller robot where moving the entire agent is not very power hungry as compared to adding another sensor by increasing it's weight and computation. 

The second approach utilizes an active sensor, a sensor which only works when movement is present, such as event camera. They have a higher dynamic range and lower latency compared to classical cameras. 

The third approach brings the change of robot's body morphology to enable simpler perception. Such an approach can be used to make the robot smaller as required while uitlizing a bigger set of sensors. Such an approach is desired when moving the robot is less power efficient than adding additional components to enable the movement of the sensor suite. This project will be implement this approach to reduce amount of sensors, and directy estimating depth and positions. 

The last approach utilizing a method which hallucinates an active observer. The simple example is the headmap of interest areas. Such a method is computationally more expensive but can be utilized when power used computation is far lesser than moving the agent or a part of it. This project will implement this technology as well, by using single Lidar and single camera sensor suite. 

### Hardware and Software Co-design
“People who are really serious about software should make their own hardware.” by Alan Kay, a pioneer computer scientist quoted in the 1980s. The "Embodied AI" research field is trying to solve this multidimensional optimization problem across different strates(hardware and software). Therefore, we are going to define the size, Weight, Area and Power (SWAP) constrains. 

### Size, Weight, Area and Power
The first prototype will be based on a tank drive style wheel chair chassis, it will be very close to the target vehicle platform.  
1. Size. The chassis is 1000mm in length, 600mm in width and 1200mm to 1800mm in height. It can easily go throught most 28-34in wide door ways. The Human Machine Interface, the touch screen can be adjusted at chirdren or adult eye level height. 
2. Weight. There is not weight constraint. Therefore, we can use Lead-Acid batteries, and desktop PC for maximum power range and computing power. Payload: 300 lbs. 4 point lifting loop. 
3. Area. The footprint of the robot is 0.6 square meter.
4. Electrical power supply. 2 - 70AH batteris. Up to 15km driving range, max speed 6 MPH, faster then Gas powered tank drive, and 2 hours run time. 

5.The wheel chair platform come with OEM control, try to integrate with standard RC controller. 

6. Build the Controller enclosure, Power distribution, fuse, DC-DC converter, waterproof connectors, the Emergency stop push button and wire, operation beacon light, GPS and Wifi, on board computer and other parts as needed.
7. I assume the lawn mower is using generic PWM Radio Control servo, I will manage the output signal is able to drive standard RC servo. One channel for Forward/Backward, one channel for Left/Right. Plus 5 channel digital channels, on and off for cutter up/down.  
8. I am going to use cameras and lidar to detect obstacle, and unexpected events. Many special designed traffic cones needed to mark the working area for safety and SLAM propose. 
9. I am going to have a hign spec processing computer off the machine, to handle the initial boundary waypoint setup (Geofencing), the detailed path waypoint(0.2m-0.5m resolution) calculation, and provide base GPS location and Wifi access point. This computer may handle more than one robot in the same area. The computer is mounted on the service truck, the service truck hauls all robots to the working zone, fuel the robots, and charging batterise as needed. 

## Hign Level Design Concept: 

The active design is useful for low-latency applications such as moving robot. The active mechanism on a large enough robot(with enough SWAP constraints for a myriad of sensors) can act as a failure mechanism when one or more of the sensors fail. The active mechanism also can move to explore the world to gather more information for a confident preduction. 

The first prototype's smallest size is 600mm width, therefore, it can carry some expensive and bulky passive sensor, but it is better to have some active sensors to reduce the size, cost and overall performance.  



Following each assumptions, I calculated requirments and souring the parts for this project. 
1. Given power budget 24V 4A total power consumption for the onboard computer and sensors, a 20V 9AH hour battery can provide 1 hour of run time.

2. 300mmx400mmx170mm waterproof box is suitable for the controller enclosure. See details of all components in the cost estimate. 

3. The Jetson Nano Developer Kit 4G version may have enough power to handle sensor data colletion, and motion control functions. Using usb - servo adapter to provide the PWM signals. 2 channels at this point. Necessary HAT or termial blocks will added to the system. 
![jetson-nano-dev-kit-top-r6-HR-B01](https://user-images.githubusercontent.com/22917810/128587074-09dd9710-b499-4af4-850c-7c8590eb90f8.png)

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

## Programming
The demo system should use hybrid ROS/ROS2 environment. My onboard computer is Nvidia Jetson Family. Original candidate is Jetson Nano 4GB Version, because of the native Linux Ubuntu environment, support ROS, and Rasberry Pi GPIO interface. Possible implemtation of GPU accelerated Point Cloud Library and opencv library. Hardware vendor may provide ROS2 driver already, it will greatly shorting the developing duration. There are more previous developed motion planning node, Vision sensor, Lidar and Mapping , PID controller, MPC controller, GNSS module, sensor fusion node etc need be tested on ROS or ROS platform. ![Block+Diagram1](https://user-images.githubusercontent.com/22917810/128586890-db5f8164-6a25-4559-944e-855cb03bf478.png)
 
I design the lawn mower as a slave device. The master device send serise of waypoints, the slave device will based on its current position, calculate the lowest cost route to reach the next waypoint, until all waypoints are reached. The lawn mower carries GPS, Lidar, camera and short distance safety sensors. Safety sensors and relays are the fail safe plan to make sure the lawn mower is safe to operate in public area, and supervise the nondeterministic AI program to meet functional safety standard ISO 26262.

I breakdown the programming scope of work into the following: 
1. Motion control. (Input: Planned waypoints, in Long, Lat, Heading, Speed, Accelation, tool up/down ... format, EGO position, in Long, Lat format; Onboard processing: Calculate the best route that can reach all the waypoints as close as possible and go as smooth as possible. Also can handle the communication delay 300ms up to 3 seconds. Output(Pending, waiting for actual machine arrive: Left/Right, Forward, Stop, Up/Down).
2. Main Loop: 100ms spin cycle. Allign with GPS update interval, Lidar frame rate, camera frame rate, watch dog program. The onboard Controller time is synchronized to GPS time. All Lidar point cloud data, IMU data, and camera image and other sensor data are timestamped and recorded in ROS bag format for future development.
3. GPS/GNSS/IMU unit: Integrate the ROS driver into the system via USB or RS232 port or GPIO pins. Time Sync. Output: Current location Long Lat format. IMU raw input at 100HZ to 200HZ, accelation and gyro reading for XYZ axises, use sensor rack slide motion(Pan, Tilt, and slide) to calibrate the IMU data. Output: The past smooth trajectory up to 200 points/second, transformed into UTM format. 
4. Lidar: Integrate the ROS driver into the system, configure the Ethernet port. Input: Up to 480000 points/sec, dual return at 15º FOV , local coordinate. Raw IMU output at 200 HZ. GPS location at 10 HZ. Processing: Register the point cloud for 0.1s to 1sec. Extract the landmark features with GeoTag. Online SLAM to calculate the robot path and heading. Output: Current heading, log the landmarks features. 
5. Camera: Integrate the ROS driver into the system, configure the Ethernet port. Input: Color RGB image, 1920x1080 pixels or better, 10-30FPS, same  15º FOV as Lidar, Geotaged landmark features. Processing: Extract the color images for the landmarks, timestamp and geotag the transformed landmark location. Recognize the QR code and corners of landmark. Output: List of landmarks with unique ID. 
6. Sensor fusion/SLAM: Input: Timestamped Landmarks point clouds transformed into UTM format. Timestamped RGB image of those landmarks with geotag on UTM format. Current state: Position, Speed, heading, surrounding features. Processing: Overlap the Landmark points clouds to create surrounding heatmap, create the equations for the conditions, solve the equations, get the current location estimate. Output: Current location estimate within 0.3m accuracy. 
7. Geofence training/setting: Walk or drive alone the boundary, about 50mx50m area, 1 hour operation time, send the GPS recording to Master device, the central controller. Walk alone the inside island such as tree, pad, or something else you don't want to run over it. The central controller will smooth out and connect the boundarys and islands, calculate the inside path with offsets to the boundary, with some overlap on each path. Output: Serized waypoints, UTM or Long Lat format. 
8. Central controller / User interface: Include Ruggedized tablet, GPS and Wifi on the trailer, to remote control the lawn mower. View the real time video feed. Modify the geofence and regenarate the path. Logging the completed work. 

## Summary Scope of Work/Deliverables
1. Meetings and tours with client to review the Project Scope
2. Mechanical design and drawings for the assembly
3. Electrical design and drawings for safety devices
4. Assembly, programming and testing of the device at my shop
5. Commissioning and testing the device at field
6. Training on how to operate new device
7. Complete documentation including spare part list

## Factory Acceptance Test
FAT will be held at my shop to demonstrate and prove operation of the device

## Commissioning / Site Acceptance Test
Site Commissioning Service will be provided. 4G vision will be responsible for on-site preparation work, traffic cones and trailers. 

## Training
Training will be provided during the commissioning and SAT phase. 

## Support Service
Additional support service are available as per agreeed rate schedule. 

## Drafting / As-built Drawings
Mechanical drawings: Sensor mount, tooling
Electrical drawings: Panel wiring, interface cable pinouts.

## Spare Part List
Upon Request

## Questions and Clarifications
Estimated delivery will be 8 months. Due to the availability of certain parts and software developments:
- The lawn Mower (2-3 months delivery)
- Electrical/Control Panel (Short supply of computer chips)

## Cost Estimate
See attached spreadsheet
