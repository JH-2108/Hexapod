# Bluetooth-controlled hexapod robot 
An 18-degree-of-freedom (18-DOF) hexapod robot featuring six articulated legs, an ESP32 microcontroller, and bluetooth based smartphone control. The robot will use custom 3d printed mechanical components designed around MG90S metal-geared micro servos. 

# Project Overview 
This project aims to build a lightweight, six-legged walking robot that can be controlled wirelessly from a smartphone. The chassis, leg segments, and servo mounts will be designing in CAD and manufactured using 3D printing. 

The robot will use coordinated servo movement and a tripod walking gait to achieve stable locomotion on suitable flat surfaces. 

# Features 
- **Six articulated legs**: Three servo controlled joints per leg, providing 18 degrees of freedom.
- **Bluetooth control**: Wireless movement commands from a compatible smartphone.
- **Custom mechanical design**: 3D-printed chassis, leg segments, and servo mounts.
- **Programmable movement**: Forward, backward, turning, and stopping, with additional movements explored during the development.
- **Compact electronics**: ESP32-based control with dedicated PWM servo drivers.

# Hardware 
| Component | Quantity | Purpose | 
|---|---|---|
|ESP32 development board| 1 | Main controller and Bluetooth communication | 
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
The ESP32 will receive movement commands over Bluetooth and calculate the required joint positions. 

The two PCA9685 boards will provide 18 independent servo control channels through the I2C interface. 

The system will use separate regulated supplies for the servo power rail and controller logic. All control signals will share a common ground reference. 

The power system will include appropriately rated wiring, connectors, a main switch, and electrical protection. 

# Software Plan 
The firmware will be developed incrementally: 
1. Establish bluetooth communication between the smartphone and ESP32.
2. Test individual servo positions and calibrate joint limits.
3. Configure both PCA9685 drivers.
4. Implement inverse kinematics for foot positioning.
5. Develop a tripod walking gait.
6. Map smartphone controls to movement commands.
7. Test turning, stopping, and basic directional movement.
8. Tune gait timing and joint positions for stability.

The smartphone interface and communication protocol will be selected during implementation. 

# Safety and Limitations 
The MG90S is a small servo intended for lightweight mechanisms. The robot's total mass, joint geometry, and servo torque will be determine whether it can support its own weight reliably. 

Initial tests will be performed with the robot supported and with individual legs tested before full walking trials. Servo stall conditions, excessive heating, unstable power and mechanical binding will be avoided. 

The initial version is intended for controlled indoor demonstrations on suitable flat surfaces, not autonomous navigation or operation over difficult terrain. 



