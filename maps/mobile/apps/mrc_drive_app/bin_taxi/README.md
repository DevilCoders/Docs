## Compile
```
ya make \
    --maps-mobile \
    --target-platform=default-linux-aarch64 \
    -r --lto \
    -DNO_GRAPHICS \
    -DNO_DEBUGINFO \
    -DSTRIP=yes \
    -DCFLAGS=-fno-asynchronous-unwind-tables \
    --build=minsizerel
```

## Run
```
YANDEX_MAPS_SIGNALQ_DEVICE_ID=my_device_id \
[YANDEX_MAPS_RUNTIME_LOGGING_LEVEL=info]   \
[YANDEX_MAPS_RUNTIME_HOSTS_ENV=testing]    \
./mrc-taxi-app
```

## Analyze binary with ya bloat
1. Generate lld file:
```
ya make \
    --maps-mobile \
    --target-platform=default-linux-aarch64 \
    -r --lto \
    -DNO_GRAPHICS \
    -DNO_DEBUGINFO \
    -DSTRIP=yes \
    -DCFLAGS=-fno-asynchronous-unwind-tables \
    --build=minsizerel \
    --target-platform-flag DUMP_LINKER_MAP
```

`mrc-taxi-app.map.lld` file will be generated.

2. Run ya bloat:
```
ya tool bloat -m mrc-taxi-app.map.lld --input mrc-taxi-app
```

3. Open `<host>:8000` in browser.
