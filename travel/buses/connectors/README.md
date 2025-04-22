# Коннекторы автобусов

### Development
1. Fetch all environment variables from any production host
2. Create the environment file ```.env```. Example
```
SOME_NAME=SOME_VALUE
ANOTHER_NAME=ANOTHER_VALUE
```

3. Change environment variable ```YENV_TYPE``` to ```development```
4. Create local settings:
```
cp config/development.py.example config/development.py
```
5. Create the rasp_data subfolder and download settlement.bin, station.bin, settlement2station.bin and timezone.bin
resources from https://sandbox.yandex-team.ru/resources?type=DUMP_RASP_DATA_RESOURCE into it.
6. Build binary, set variables from ```.env``` and run ```bin/connector```.
7. Enjoy!

Notes:
1. Use ./bin/python as python interpreter for IDE

### Deployment

#### Manual

1. ```ya package pkg.json --docker --docker-push --docker-repository=yandex-bus --custom-version=<NEW RELEASE TAG>```
2. After that new image is available in Qloud
