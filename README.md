# Personal Configuration Document

1. GPU Name: NVIDIA GeForce RTX 2070 max-q
2. Vram: 8192 MiB
3. OS: Ubuntu 22.04.5 LTS (Jammy)
4. ROS 2: Humble
5. Driver Version: 580.82.07
6. CUDA Version: 13.0
7. cuDNN: Version 8.9.7
8. TensorRT: Version 10.8.0
9. [Awsim_labs v1.6.1](https://github.com/autowarefoundation/AWSIM-Labs/releases/tag/v1.6.1)
10. [Autoware 1.8.0](https://github.com/autowarefoundation/autoware/releases/tag/1.8.0)


# Performance Issue
had some performance issues, the car would engage emergency and break, and wouldnt let the car move, found the root and the solution in the following Awsim lab github issue.

[Self-driving Fails or Frequently Enters EMERGENCY_STOP #207](https://github.com/autowarefoundation/AWSIM-Labs/issues/207)

fixed by lowering the time scale.


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


# Common Config Files

## Changing Speed Limit
```bash
/home/msadegh/autoware/src/launcher/autoware_launch/autoware_launch/config/planning/scenario_planning/common/common.param.yaml
```

## Car Dimensions Information
```bash
/home/msadegh/autoware/src/vehicle/awsim_labs_vehicle_launch/awsim_labs_vehicle_description/config/vehicle_info.param.yaml
```


# Common Commands