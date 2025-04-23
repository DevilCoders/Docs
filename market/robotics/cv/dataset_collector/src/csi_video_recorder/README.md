# MP4 Recorder

Python Package that allow to record video from 2 CSI cameras

## Instalation

1. Create venv for launching
2. Install py_dataset_collector
3. Install csi_video_recorder
4. Launch recorder with script

```bash
mkdir -p ~/data/videos
cd ~/data/videos

python3 -m venv venv --system-site-packages
source venv/bin/activate

pip install ~/dataset_collector/src/py_dataset_collector
pip install ~/dataset_collector/src/csi_video_recorder

# Launching:
recorder
```

## Usage:

To start recording push phisical button. To stop recording push the button again

To exit, use keyboard and CTRL+C keyboard shortcut
