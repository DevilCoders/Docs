# Description

This ros python-based package is responsible for robot control. In the first itertion,
this module is also responsible for route planning. Thus, this module contains
hardcoded test maps.

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
colcon build --packages-select ymbot_robot_control --symlink-install --event-handlers console_direct+ \
    --cmake-args -DCMAKE_VERBOSE_MAKEFILE=ON
```

# Run

## Run path follower only
```bash
cd ymbot
source ./install/setup.bash
ros2 launch ymbot_robot_control robot_control_node_and_simulation.launch.py
```

This script runs robot control. It also runs rviz with test map.

# Parameters

    robot_control_node:
      ros__parameters:
        robot_control_node: responsible for node class
          map_loader: responsible for loading of virtual railway map
            file_name: name of file for railway map (str)
          map_publisher:
            topic_name: name of topic for visualization (str)
            frame_id: name of frame for map publication (str)
          rate: rate of timer for node work (float)


