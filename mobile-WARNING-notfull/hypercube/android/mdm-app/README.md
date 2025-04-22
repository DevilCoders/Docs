# android-mdm-app

Android companion app for https://hypercube.yandex-team.ru (https://st.yandex-team.ru/DEVTOOLS-5347)

Installation
============
Application needs device owner rights. [For more details](https://stackoverflow.com/questions/10904841/avoid-securityexception-because-of-no-active-admin-owned-by/49820805#49820805)

```
adb shell dpm set-device-owner com.yandex.mdm/.DeviceAdminReceiver
```

Remove restrictions (factory reset, wallpapers, etc):
```
adb shell am broadcast -n "com.yandex.mdm/com.yandex.mdm.DeviceUnrollReceiver"
```

Change device password:
```
adb shell am broadcast -n "com.yandex.mdm/com.yandex.mdm.DeviceResetReceiver" --es password 1234
```

Enable device lock on power disconnect:
```
adb shell am broadcast -n "com.yandex.mdm/com.yandex.mdm.DeviceLockReceiver"
```

Настройка девайса
============
Полная пользовательская инструкция находится [в вики](https://wiki.yandex-team.ru/hypercube/mdm/android/)

 - Включите отладку по USB и проверьте работу через `adb shell`.
 - Установите приложение по ссылке ... через `adb install app.apk`.
 - Активируйте device owner через `adb shell dpm set-device-owner com.yandex.mdm/.DeviceAdminReceiver`.
 При ошибке вида
 `java.lang.IllegalStateException: Not allowed to set the device owner because there are already some accounts on the device` удалите в настройках устройства все аккаунты и повторите активацию (не забудьте добавить аккаунты обратно после завершения!).
 - Если всё прошло успешно, то на устройствах с Android 5.0 и выше нельзя делать сброс из настроек.  
