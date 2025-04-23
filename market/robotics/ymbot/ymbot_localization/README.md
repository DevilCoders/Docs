# Description

This ros python-based package is responsible for robot localization.
This method is based on EKF (Extended Kalman Filter). This filter fuses data from
Cartographer LIDAR odometry and detected ArUco markers. For more info, look at [preliminary research about localization methods](https://wiki.yandex-team.ru/roboticsmarket/softwarearchitecture/lokalizacijadljarobota/issledovaniefiltrakalmanadljalokalizacii/).

# Build

## Prerequisite

1. Python3.8
2. ROS2 (rclpy)
3. Colcon

Python packages:

1. setuptools >= 45.2.0
2. numpy >= 1.22.2
3. scipy >= 1.8.0

## Build commands

```bash
cd ymbot
source /opt/ros/foxy/setup.bash
colcon build --packages-select ymbot_localization --symlink-install --event-handlers console_direct+ \
    --cmake-args -DCMAKE_VERBOSE_MAKEFILE=ON
```

# Run on rosbag

```bash
cd ymbot
source ./install/setup.bash
ros2 launch ymbot_localization run_localization_rosbag.launch.py \
  rviz_config:=$RVIZ_CONFIG rosbag:=$ROSBAG \
  landmarks_config:=$LANDMARK_CONFIG camera_config:=$CAMERA_CONFIG
```

This script run ymbot_localization on the input rosbag. rviz_config -
path to rviz config. landmarks_config - path to localization landmarks. camera_config -
path to camera config.

