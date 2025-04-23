# Kolhoz-Client (Kotlin Native)

For user default json config rename kolhoz_konfig_exampl.json => kolhoz-config.json

<b style="color:red">If json file is set, terminal arguments will not be used !!</b>

Generate
Token [Here](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=860ca94572a7460e82c9e39c857bab77)

[Gradle Implements](https://wiki.yandex-team.ru/taxi/mobile-infra/kolhoz-gradle/)

---

Supported Commands:

1. **kolhozOcuppyDevices** - booking devices by your params
2. **kolhozReleaseDevices** - release devices booking early or specified by --devicesList
3. **kolhozReleaseAllDevices** - release all devices from your kolhoz user
4. **kolhozGetReports** - get reports from android devices
5. **help** - show how to..

---

Building binary executable file

```
./gradlew assemble - for all platforms 
./gradlew compileKotlinMacosX64 - for Mac OS 
./gradlew compileKotlinLinuxX64 - for Linux 
```

### Booking Example

```shell
kolhozOcuppyDevices
--kolhozToken=TOKEN \
--bookingTime=30 \
--allowCompletelyBooking=true \
--allowIncompleteOccupation=true \
--status=READY \
--osType=ANDROID \
--groups=TAXIMETER,TAXI \
--deviceType=PHONE \
--osSDKVersion=27,28,29,30 \
--assumedDeviceCount=3 \
--removeApkAfterBooking=ru.uber.driver,ru.uber.driver.test,ru.yandex.taximeter,ru.yandex.taximeter.test,ru.yandex.taximeter.beta,ru.yandex.taximeter.beta.test  \
--occupyTimeoutMinutes=1
```

### Release From File (After Booking) Example

```shell
kolhozReleaseDevices \
--kolhozToken=TOKEN \
--devicesList=deviceId1,deviceId2
```

### Release All Devices Example

```shell
kolhozReleaseAllDevices \
--kolhozToken=TOKEN
```

### Get Report From Devices Example

```shell
kolhozGetReports \
--kolhozToken=TOKEN \
--devicesList=deviceId1,deviceId2 \
--reportPathList=(sdcard/allure-results:./) 
```





