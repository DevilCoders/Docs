# Dataset collector

## Dependencies

1. `ROS2`
2. `colcon` build system
3. `ros2bag`: (To install use the following command (ubuntu-jetson): `sudo apt install -y ros-eloquent-ros2bag ros-eloquent-rosbag2-converter-default-plugins ros-eloquent-rosbag2-storage-default-plugins`)

## Build scripts

In the source direcotry with the following structure:

```bash
.
├── README.md
├── helpers
└── src
```

execute the folloing script to build:

```bash
colcon build --packages-select py_dataset_collector
```

## Launch scripts

```bash
. install/setup.bash 
ros2 launch py_dataset_collector collector.launch.py
```

or use `helpers/init_collector.sh`

### Available topics in /collector namespace after launching

```bash
/collector/buttons
/collector/frame0
/collector/frame1
/collector/parameter_events
/collector/record_state
/collector/rosout
```

## Helpers

### Image viewer

It doesn't work with CompressedImage message type

```bash
ros2 run image_tools showimage --ros-args -p reliability:=best_effort /
```

### Visualizer

```bash
ros2 run dataset_collector visualizer_node
```

### Systemd unit for autostart

There are 2 ways of systemd unit initialization:

1) Send `DISPLAY=:0` enviroment variable to launch directly with display parameter
2) Make delay with `ExecStartPre=/bin/sleep 5` to wait for initialization

#### Setup

```bash
cp helpers/collector.service $HOME/.local/share/systemd/user/
systemctl --user daemon-reload
systemctl --user enable collector.service 
systemctl --user restart collector.service
```

#### Status

```bash
systemctl --user status collector.service
```

### Frame saver v 0.0.1

Frame saver is a special package that allow to save jpg frames from topic with CompressedImage.

#### Build

To build the package use the following command line script

```bash
colcon build --packages-select py_frame_saver
```

#### Launching

```bash
ros2 run py_frame_saver frame_saver_node --ros-args -r frame:=/collector/frame0
```

#### Parameters

- with_visualisation [Bool], allow to show input frame **NOT SUPPORTED YET**
- queue_size [Int], queue size of subscriber
- out_folder [String], path to folder to save images
- format [String], out image format

#### Using of Docker as pipeline for parsing rosbag2 files

The following *.sh script launch Dockerfile on ros foxy image, build py_frame_saver.
Launch this file in `dataset_collector` folder

```bash
/bin/bash helpers/frame_saver/parseBagFiles.sh -f bag_files/rosbag2_2022_02_16-17_19_16 -o ./parsed_data
```

To see man for script use `-h` flag

```bash
/bin/bash helpers/frame_saver/parseBagFiles.sh -h
```

## Video recorder

Another approach to collect frames is to use `csi_video_recorder`. Additional info in `./src/csi_video_recorder/README.md`