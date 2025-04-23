# [Tier 1] embedded

## Requirements

+ Arm GNU Toolchain
+ OpenOCD
+ make

## Quick start

1. Find supported platforms

    ```bash
    cd nuttx
    ./tools/configure.sh -L | grep uros # Find all configurations with preconfigured micro-ROS
    ./tools/configure.sh -l nucleo-h743zi2:uros # Select the configuration
    ```

2. Build the project

    ```bash
    make
    ```

    As a result you should get binary artefacts of the built firmware: nuttx.bin, nuttx.hex
