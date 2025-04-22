# Description

This ros python-based package is responsible for robot behaviour. The core of the
robot behaviour is behaviour tree
(https://wiki.yandex-team.ru/roboticsmarket/softwarearchitecture/behaviou-tree/)
This package contains a node for behaviour tree.

# Build

## Prerequisite

1. Python3.8
2. ROS2 (rclpy)
3. Colcon

Python packages:
1. setuptools >= 45.2.0
2. numpy >= 1.22.2
3. scipy >= 1.8.0

ROS packages:
1. Joint statue publisher (ros-foxy-joint-state-publisher)
2. Xarco ros-foxy-xarco
## Build commands
```bash
cd ymbot
source /opt/ros/foxy/setup.bash
colcon build --packages-select ymbot_behaviour_tree ymbot_behaviour_interface \
    --symlink-install --event-handlers console_direct+ \
    --cmake-args -DCMAKE_VERBOSE_MAKEFILE=ON
```

# Test
```bash
source ./install/setup.bash
colcon test --packages-select ymbot_behaviour_tree \
  --event-handlers console_direct+ --pytest-args "-v"
```

