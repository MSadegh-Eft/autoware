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
had performance issues that, found the root and the solution in the following github issue.

[Self-driving Fails or Frequently Enters EMERGENCY_STOP #207](https://github.com/autowarefoundation/AWSIM-Labs/issues/207)

fixed by lowering the time scale.