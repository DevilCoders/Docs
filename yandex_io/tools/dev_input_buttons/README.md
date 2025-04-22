# Utility to check /dev/input/eventX buttons work

## Original
Source code is a copy from https://elinux.org/images/9/93/Evtest.c

## Usage
Usage: evtest /dev/input/eventX

Where X = input device number

## Example

```
./evtest /dev/input/event2
Input driver version is 1.0.1
Input device ID: bus 0x19 vendor 0x1 product 0x1 version 0x100
Input device name: "gpio-keys"
Supported events:
  Event type 0 (Sync)
  Event type 1 (Key)
    Event code 113 (Mute)
    Event code 114 (VolumeDown)
    Event code 115 (VolumeUp)
    Event code 207 (Play)
    Event code 237 (?)
```
Event code represent the button you can use.
Try to press any button (i.e. VolumeDown)

```
Event: time 1581065701.442281, type 1 (Key), code 114 (VolumeDown), value 1
   Event: time 1581065701.442281, -------------- Report Sync ------------
   Event: time 1581065701.629790, type 1 (Key), code 114 (VolumeDown), value 0
   Event: time 1581065701.629790, -------------- Report Sync ------------
```

If such log appear it means that this Event Code actually represent button in /dev/input/eventX node. **value 1** mean that button is pressed. **value 0** -- button released.
