# Zigbee manufacturing test utility

## Prerequisites

Two devices with an attached Zigbee module: either 2 smart speakers or a smart speaker and a debug board. Zigbee modules should be running NCP firmware. For factory-flashing YandexMidi refer to https://wiki.yandex-team.ru/smartdevices/midi/zigbee/factory/.

## Building

```
$ ya package smart_devices/tools/zigbee_mfg_test/package.json --raw-package-path zigbee_mfg_test
```

## Usage

1. Start test server on the first device
   ```
   $ zigbee_mfg_test server --port /dev/ttyACM0 --channel 11 --power 10 --session 42
   [2021-08-30 20:08:45.783] [info] [main.cpp:139] Listening for test frames on channel 11
   ```

2. Run test client on the second device
   ```
   $ zigbee_mfg_test client --port /dev/ttyS3 --channel 11 --power 10 --num 10 --session 42 --report test.json
   [2021-08-30 19:48:29.703] [info] [main.cpp:207] Sending 10 packets on channel 11
   [2021-08-30 19:48:29.862] [info] [main.cpp:222] Waiting for response
   [2021-08-30 19:48:34.964] [info] [main.cpp:280] Packet 0 OK LQI 160 RSSI -60
   [2021-08-30 19:48:34.965] [info] [main.cpp:280] Packet 1 OK LQI 164 RSSI -59
   [2021-08-30 19:48:34.965] [info] [main.cpp:280] Packet 2 OK LQI 164 RSSI -59
   [2021-08-30 19:48:34.965] [info] [main.cpp:280] Packet 3 OK LQI 164 RSSI -59
   [2021-08-30 19:48:34.965] [info] [main.cpp:280] Packet 4 OK LQI 168 RSSI -58
   [2021-08-30 19:48:34.965] [info] [main.cpp:280] Packet 5 OK LQI 168 RSSI -58
   [2021-08-30 19:48:34.965] [info] [main.cpp:280] Packet 6 OK LQI 168 RSSI -58
   [2021-08-30 19:48:34.965] [info] [main.cpp:280] Packet 7 OK LQI 168 RSSI -58
   [2021-08-30 19:48:34.965] [info] [main.cpp:280] Packet 8 OK LQI 168 RSSI -58
   [2021-08-30 19:48:34.965] [info] [main.cpp:280] Packet 9 OK LQI 168 RSSI -58
   [2021-08-30 19:48:34.965] [info] [main.cpp:299] Error rate: 0%
   [2021-08-30 19:48:34.965] [info] [main.cpp:300] LQI: min 160 avg 166 max 168
   [2021-08-30 19:48:34.965] [info] [main.cpp:301] RSSI: min -60 avg -58.5 max -58
   [2021-08-30 19:48:34.965] [info] [main.cpp:308] Test report saved to test.json
   ```
