# Description

This ros python-based package is responsible for robot navigation. It contains
node for path following. The main algorithm for path following is Samson
Path Follower.

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
colcon build --packages-select ymbot_navigation --symlink-install --event-handlers console_direct+ \
    --cmake-args -DCMAKE_VERBOSE_MAKEFILE=ON
```

# Run

## Run path follower only
```bash
cd ymbot
source ./install/setup.bash
ros2 launch ymbot_navigation path_follower.launch.py
```

This script runs path follower only launch file. It loads configs from
config/path_follower.yaml and runs path follower node. Configured for autostart with
NUC container.

## Input topics
1. path - input path
2. tf transform form ymbot to map

## Output topics
1. cmd_vel - output velocity topic

# Parameters

    path_follower_adapter:
      path_follower:
        intermediate_goal_threshold: Intermidate Goal threshold
        maximal_linear_velocity: Maximal linear velocity
        maximal_angular_velocity: Maximal angular velocity
        path_follower:
          goal_approacher:
            type: Type of goal approacher
            k_p: Proportianal koeficient for deceleration
            approach_distance: Distance when approacher is activated
            parameter_threshold: Threshold for trajecotyr parameter
            distance_threshold: Threshold for distance
            angle_threshold: Threshold for angle difference
            p_angle_koef: Proportional koefficient for angle
            maximal_angular_velocity: Maximal angular velocity
          maximal_linear_velocity: Maximal linear velocity
          maximal_angular_velocity: Maximal angular velocity
          k_alpha: alpha koefficient for Samson Regulator
          k_beta: beta koefficient for Samson Regulator
          time_delay: time delay koefficient for Samson Regulator
          maximal_angle: Maximal angle for rotation without moving
          maximal_angle_koef: Maximal angle koefficient for rotation moving
          velocity_angle_koef: Velocity angle koefficient for rotation moving
          use_sinc: Use sinc for Samson regulator
          use_arctan: Use arctan for Samson regulator
      trajectory_factory:
        direction_threshold: Direction threshold for new trajectory segment
        angle_threshold: Angle threshold for new trajectory segment
        trajectory_factory:
          from_positions: Load from positions
          from_points_with_direction: Load from points
          minimal_distance: Minimal distance
      robot_state:
        base_frame: Base frome
        parent_frame: Map frame
      trajectory_publisher:
        trajectory_topic: Path topic name
      rate: rate for node
      velocity_topic_name: elocity topic name
      action_name: action topic name
      debug: debug or not
