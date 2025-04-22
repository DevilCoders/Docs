# Simple test node for performance analysis

## Requirements

1. ROS 2 Foxy
2. micro_ros_agent

## Nodes

- `perf_relay` - a simple publisher/subscriber node which relays the header of incoming `sensor_msgs/Imu` to the outcoming `std_msgs/Header`.

  It is used to measure Round-trip time (RTT) for the microcontroller connection.

  - Publisher: `/microROS/feedback`
  - Subscriber: `/microROS/data`

  Dependant node located at `/market/robotics/embedded/apps/ymbot/perf_test`

## Examples

### Running __perf_relay__ node

```bash
ros2 run microros_perftest_relay perf_relay
```

### Micro-ROS Agent using UDP transport layer

```bash
ros2 run micro_ros_agent micro_ros_agent udp4 --port 8888
```

### Micro-ROS Agent using Serial transport layer

```bash
ros2 run micro_ros_agent micro_ros_agent serial --dev /dev/ttyACM0
```

### Micro-ROS Agent build example

```bash
mkdir temp && cd temp # Assuming that you are in the market/robotics root directory
. ../ymbot/ymbot_ll/scripts/build_agent.sh \
    --base-paths ../libs/main/ ../libs/micro/micro_ros_msgs/ ../tools/ament/ \
    --build-base ./build \
    --install-base ./install
```
