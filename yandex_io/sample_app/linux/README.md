# Simple Linux Sample App

## Prepare

1) Build sample app:
```
cd ARCADIA_ROOT/yandex_io/sample_app/linux
ya make -DUSE_DYNAMIC_ALSA
```
Contrib alsa lib crashes, so we use system libasound.

2) Build config:
```
cd ARCADIA_ROOT/yandex_io/sample_app/linux/config
ya make
```
3) Build helper, that will provide xCode for the first time configuration
```
cd ARCADIA_ROOT/yandex_io/tools/get_oauth_code
ya make
```
## First Configuration
By default sample_app will ask to register in backend after dry start. It's standard behaviour for devices, so sample_app wait's for R2D2/BLE configuration. But can be tricky with sample_app (it can't configure wifi networks, so firstrund service may be not happy). To avoid this issue has special ```--authcode``` flag which is used to register sample_app in quasar backend bypassing R2D2/BLE setup. ```--authcode``` takes xCode as an argument. It is a special code generated via passport api using user token

So run:
```
./sample_app --authcode SOME_X_CODE
```

```get_oauth_code``` is a helper tool that will generate xCode using SessionId cookie.
### How to use:
```
./get_oauth_code xcode --sessionid "COOKIE"
```
Note: Cookie should be wrapped with quotes. Use cookie once for registration SampleApp's device-id in test-backend.

Result:
```
>>> [DATE_TIME] INFO     root       xcode is <[SOME_X_CODE]>
```
SOME_X_CODE value is a required argument for ```sample_app --auth SOME_X_CODE ```
Use xcode once for registration SampleApp's device-id in test-backend.

### Multiple instances of sample_app on one machine
To test multiroom/stereopair/tandem functionality.

1. Generate two different quasar.cfg files with different ports for every daemon.
2. Specify different workdir pathes in ```"patterns":{ "DATA":...}``` cfg field
3. Run different SampleApps with different ```--device-id UNIQUEDEVICEID``` parameters
4. Specify connectivity neighbors via ```--use-glagol --neighbor DEVICEID1:PORT1 --neighbor DEVICEID2:PORT2```. Where PORTN is "externalPort" field from "glagold" section of quasar.cfg of DEVICEIDN.

### Registration result
**If sample_app successfully registered in backend, there is no need to use ```--auth``` argument until token will expire or workdir will be removed**

## Logging
By default sample_app follow rules from ["yiod"]["Logging"] section of config. To enable logs to stdout use ```--logs-to-stdout``` sample_app argument
```--logs-to-stdout``` may take and argument with log level (trace, debug, info, warn, error). If flag is used without argument -- debug is used by default

## Environment
Sample app prepare environment for it's work:

1) Create and enter "workdir"

2) Set up FD limit up to 3072

**NOTE:** Core files will be also dumped into workdir (if default core pattern path is used)
