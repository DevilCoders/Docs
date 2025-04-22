## Local mode

```bash
# build
ya make
# list available services
SANDBOX_CONFIG=../etc/settings.yaml ./sandbox-services list
# run some service
SANDBOX_CONFIG=../etc/settings.yaml ./sandbox-services run --name mongo_monitor --stderr-log
```
