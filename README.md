# Bluetooth-controlled hexapod robot 
An 18-degree-of-freedom (18-DOF) hexapod robot featuring six articulated legs, an ESP32 microcontroller, and bluetooth based smartphone control. The robot will use custom 3d printed mechanical components designed around MG90S metal-geared micro servos. 

# Project Overview 
This project aims to build a six-legged walking robot that can be controlled using a USB game controller connected directly to the robot. 

The controller's joystick axes and button inputs will be read through a USB host interface. The ESP32-S3 will interpret those inputs and calculate the required joint movements, while dedicated PWM servo drivers control the robot's 18 servos. 

The chassis, leg segments, and servo mounts will be designed in CAD and fabricated using 3D printing. 

# Features 
- **Six articulated legs**: Three servo controlled joints per leg, providing 18 degrees of freedom.
- **USB bluetooth control**: Direct USB connection between a compatible game controller and the robot.
- **Custom mechanical design**: 3D-printed chassis, leg segments, and servo mounts.
- **Programmable movement**: Forward, backward, turning, and stopping, with additional movements explored during the development.
- **Compact electronics**: ESP32-based control with dedicated PWM servo drivers.
- **Embedded control**: ESP32-S3 interprets gamepad inputs and generates movement commands. 

# Hardware 
| Component | Quantity | Purpose | 
|---|---|---|
|ESP32 development board| 1 | Main controller and Bluetooth communication | 
| USB game controller | 1 | Wired movement input | 
| USB host connector and interface | 1 | Connects the game controller to the robot | 
| MG90S metal-geared servo | 18 | Three joints per leg | 
| PCA9685 16-channel PWM driver | 2 | Servo signal generation | 
| Rechargeable battery | 1 | Portable power | 
| High-current servo power regulator | TBD | Supply power to the servos 
| Logic voltage regulator | 1 | Power the controller | 
| Custom 3d printed chassis and legs | 1 set | Mechanical structure | 
| Screw, nuts, wiring, connectors | As required | Assembly and electrical connections. 

**Note**: The final battery, regulators, wiring and protection components will be selected after estimating the combined servo load. The servos will have a separate power rail from the ESP32 logic supply, with a common ground. 

# Mechanical design
The mechanical assembly will consist of a central body and six independently articulated legs. 

Each leg will contain three joints: 
1. **Coxa**: Rotates the leg relative to the body.
2. **Femur**: Raises and lowers the upper leg segment.
3. **Tibia**: Positions the lower leg segment and foot.

The CAD design will use the MG90S servo's verified dimensions and mounting geometry. STEP models will be used where available to align servo mounts, horn connections, and surrounding printed parts. 

The design will prioritize low weight, accessible electronics, sufficient ground clearance, and straightforward maintenance. 

# Electronics Architecture 
The ESP32-S3 will operate as the USB host and read inputs from the connected game controller. 

The control pipeline will be: 
1. The game controller sends joystick and button reports over USB.
2. The ESP32-S3 interprets the controller inputs.
3. The firmware converts those inputs into movements and gait commands.
4. The ESP32-S3 communicates with the two PCA9685 boards over I2C.
5. The PCA9685 boards generate the control signals for the 18 servos.

The USB host interface will be configured according to the selected development board. A suitable connector and host-compatible wiring or adapter will be used as required. 

The servo power rail will be separate from the controller logic supply, with a common ground reference. The power system will include appropriately rater wiring, connectors, a main switch, and electrical protection. 

# Software Plan 
The firmware will be developed incrementally: 
1. Initialize USB host support on the ESP32-S3.
2. Detect the connected game controller.
3. Read and interpret joystick axes and button inputs.
4. Configure both PCA9685 drivers.
5. Test individual servo positions and calibrate joint limits.
6. Implement inverse kinematics for foot positioning.
7. Develop a tripod walking gait.
8. Map gamepad inputs to movement commands.
9. Test forward, backward, turning and stopping.
10. Tune gait timing and joint positions for stable movement. 

The exact USB HID handling implementation will depend on the selected game controller. 

# Proposed Gamepad Mapping
|Gamepad Input | Robot function | 
|---|---|
|Left stick vertical | Forward and backward movement | 
| Left stick horizontal | Turn left and right | 
| Right stick | Optional movement or gait adjustments | 
| Face buttons | Select additional movement functions | 
| Start button | stop or pause movement, subject to controller mapping | 

# Safety and Limitations 
The MG90S is a small servo intended for lightweight mechanisms. The robot's total mass, joint geometry, and servo torque will be determine whether it can support its own weight reliably. 

Initial tests will be performed with the robot supported and with individual legs tested before full walking trials. Servo stall conditions, excessive heating, unstable power and mechanical binding will be avoided. 

The initial version is intended for controlled indoor demonstrations on suitable flat surfaces, not autonomous navigation or operation over difficult terrain. 



