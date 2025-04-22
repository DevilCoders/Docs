# Build

## Prerequisite

1. Python3.8
2. ROS2 foxy (rclpy)
3. Colcon

## Build commands
Run market/robotics/tools/ymbot_platform_scripts/dataset_collector_build.sh to build dataset collector

# Run
Run market/robotics/tools/ymbot_platform_scripts/dataset_collector_run.sh to run dataset collector

# CLI Command
rosbag record doing with command:
```
bash
ros2 bag record /color/image_raw /infra1/image_rect_raw /infra2/image_rect_raw /hesai/pandar
```
where all after record are topics
