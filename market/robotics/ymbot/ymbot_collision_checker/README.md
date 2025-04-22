# Description

This ros python-based package is responsible for collision checking and velocity limiter. It has only one node which
receives unsafe velocities and outputs limited velocities. It also inputs obstacle point cloud and outputs collision
zones.

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
colcon build --packages-select ymbot_collision_checker --symlink-install --event-handlers console_direct+ \
    --cmake-args -DCMAKE_VERBOSE_MAKEFILE=ON
```

# Run

```bash
cd ymbot
source ./install/setup.bash
ros2 launch ymbot_collision_checker velocity_limiter.launch.py
```

This script runs velocity limiter launch file. It loads configs from config/velocity_limiter.yaml and runs velocity
limiter node

## Input topics

1. unsafe_debug_cmd_vel - input velocity topic
2. obstacle_points - point cloud of surrounding obstacles

## Output topics

1. safe_debug_cmd_vel - output velocity topic
2. collision_zone - visualization of collision zone

# Test

```bash
cd ymbot
source ./install/setup.bash
colcon test -packages-select ymbot_collision_checker
```

This command run unit tests for ymbot_collision_checker package
