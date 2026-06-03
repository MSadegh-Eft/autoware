# Personal Configuration Document

1. GPU Name: NVIDIA GeForce RTX 2070 max-q
2. Vram: 8192 MiB (8 GBs)
3. ram: 16 GBs
4. OS: Ubuntu 22.04.5 LTS (Jammy)
5. ROS 2: Humble
6. Driver Version: 580.82.07
7. CUDA Version: 13.0
8. cuDNN: Version 8.9.7
9. TensorRT: Version 10.8.0
10. [Awsim_labs v1.6.1](https://github.com/autowarefoundation/AWSIM-Labs/releases/tag/v1.6.1)
11. [Autoware 1.8.0](https://github.com/autowarefoundation/autoware/releases/tag/1.8.0)

<br><br>

# Performance Issue
had some performance issues, the car would engage emergency and break, and wouldnt let the car move, found the root and the solution in the following Awsim lab github issue.

[Self-driving Fails or Frequently Enters EMERGENCY_STOP #207](https://github.com/autowarefoundation/AWSIM-Labs/issues/207)

fixed by lowering the time scale.

<br><br>

# Launch Commands

## Terminal 1 — Start AWSIM
```bash
cd ~/AWSIM/awsim_labs_v1.6.1
./awsim_labs.x86_64
```
Wait for the simulator window to fully load.

## Terminal 2 — Start Autoware
```bash
cd ~/autoware
source install/setup.bash

ros2 launch autoware_launch e2e_simulator.launch.xml \
vehicle_model:=awsim_labs_vehicle \
sensor_model:=awsim_labs_sensor_kit \
map_path:=/home/msadegh/autoware_map/nishishinjuku_autoware_map \
launch_vehicle_interface:=true
```
Wait until all nodes finish starting.

## Terminal 3 — Engage the vehicle (can also just press "Auto" in Autoware)
```bash
cd ~/autoware
source install/setup.bash

ros2 topic pub /autoware/engage \
autoware_vehicle_msgs/msg/Engage \
'{engage: true}' -1
```
That command tells Autoware to start autonomous driving inside AWSIM.

<br><br>

# Common Config Files

## Changing Speed Limit
```bash
/home/msadegh/autoware/src/launcher/autoware_launch/autoware_launch/config/planning/scenario_planning/common/common.param.yaml
```

## Car Dimensions Information
```bash
/home/msadegh/autoware/src/vehicle/awsim_labs_vehicle_launch/awsim_labs_vehicle_description/config/vehicle_info.param.yaml
```

<br><br>

# Common Commands


<br><br>


# What to keep vs replace

## [High-level architecture design](https://tier4.github.io/autoware-documentation/tier4-main/design/autoware-architecture/)

<img width="867" height="509" alt="image" src="https://github.com/user-attachments/assets/3ac127d5-0b63-4dbd-a179-44fb726b3152" />

<br>

## [Full Node diagram](https://tier4.github.io/pilot-auto-ros2-iv-archive/tree/main/design/software_architecture/NodeDiagram/)

<img width="2971" height="1661" alt="image" src="https://github.com/user-attachments/assets/1156fc0c-194b-4c2a-82f0-8b23650f63a6" />

<br>

## HD-map-based setup

<img width="1440" height="1240" alt="image" src="https://github.com/user-attachments/assets/db39c5f4-4722-4c6e-9428-f8a78e2743b4" />

<br>

## HD-map-free setup (ORION-style)

<img width="1440" height="1120" alt="image" src="https://github.com/user-attachments/assets/3d445236-2611-4ba1-96f2-eb7c8db759f3" />

