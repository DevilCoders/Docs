# Description

This ros python-based package is responsible for simulation and artificial tests.

# Build

## Prerequisite

1. Python3.8
2. ROS2 foxy (rclpy)
3. Colcon

Python packages:
1. setuptools >= 45.2.0
2. numpy >= 1.22.2
3. scipy >= 1.8.0

## Build commands
```bash
source /opt/ros/foxy/setup.bash
colcon build --packages-select ymbot_simulation_interface ymbot_behaviour_interface ymbot_navigation_interface \
    ymbot_simulation ymbot_utils ymbot_navigation ymbot_collision_checker ymbot_behaviour_tree ymbot_robot_control \
    --symlink-install \
    --event-handlers console_direct+ --cmake-args -DCMAKE_VERBOSE_MAKEFILE=ON --cmake-clean-cache \
    --allow-overriding ymbot_simulation ymbot_simulation_interface

```

# Run

## Run path follower only
```bash
cd ymbot/ymbot_simulation
source ./install/setup.bash
ros2 launch ymbot_simulation simulation.launch.py
```
# CLI Command
Before type any command do:
```bash
source /opt/ros/foxy/setup.bash
source ./install/setup.bash
```

To set mast extension type
```bash
ros2 action send_goal /mast_action_server ymbot_simulation_interface/action/MastAction "{mast_extension: extension_in_meters}"
```
