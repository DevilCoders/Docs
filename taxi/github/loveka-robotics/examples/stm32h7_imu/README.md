## Example project

### Used devices
MCU: NUCLEO-H745ZIQ-C01
IC: ICM-20602
Breadboard: London Demo

### Description
This project demonstrates how to use
London Demo board with IMU and NUCLEO H7.

It contains two project together. For both cores.
CM4 is not used and stays free.
CM7 is main project

### Toolchain
STM32CubeIDE

### Build and run
1) Preprare hardware accroding Used devices section
2) Import project to STM32CubeIDE
3) Add launch configuration for CM7
4) Build and flash
5) Open VCP on PC and see output (/dev/ttyAC0 on Ubuntu)


### More
See wiki https://wiki.yandex-team.ru/lavka/dev/robolab/imudriver/


