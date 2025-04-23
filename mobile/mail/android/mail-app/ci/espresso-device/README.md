1. Docker container with Android sdk is run in zomb-persmob-qa. In dockerfile we have portforwarding command, which forward device port inside
 the container on the same port number on Hub (mobpers-browser-gate.haze.yandex.net) at once when container is created. Dockerfile and other scripts
 are in the appium project now; Also we have file (also in appium project - main.yml) that map device id and it's port (port per device)
 (port range 5050-5100) inside the container.
2. Then we have the range of available ports (TCP from TC agents to Hub ) (ports range is the same: 5050-5100).
 Adb can be run with parameters -P - port and -H - host.
3. On TC we create 1 variable - device version, which we can choose. In .sh script we map each device version with device port
(the same as in file main.yml). And also adb command from TC is available for device (connected to zomb) if run it with -P (device port from the map)
and -H (host mobpers-browser-gate.haze.yandex.net)
