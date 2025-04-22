# Common utils for uC communication

## DR.Control controller interface converter

Converts set velocity commands for successful communication between ROS2 and Yandex Rover controller.

```bash
ros2 launch drcontrol_convert node.py
```

## Micro-ROS relay node for performance test

A simple node which ping-pongs a header with a timestamp to verify built-in synchronization and delays between a PC and uC.

### Execution

```bash
ros2 run microros_perftest_relay perf_relay
```
