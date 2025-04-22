## Build App
Первый раз
```
./gradlew :centaur-app:assembleDemoV8Debug
```
Последующие разы можно собирать командой
```
./gradlew :centaur-app:assembleDemoV8Debug  -Pdisable-external-builder
```

## Install App on local device(with adb)
```
./gradlew :centaur-app:installDemoV8Debug  -Pdisable-external-builder
```

## Launch Demo App (with debug auth)
```
$ adb shell am start -n ru.yandex.quasar.centaur_app/.MainActivity --es "token" "AgAAAAA...." --es "uid" "9....."
```

## Acquire Tokens

Для получения данных собираем https://a.yandex-team.ru/arc/trunk/arcadia/yandex_io/tools/get_oauth_code, смотрим в браузере куку `SessionId` с домена `yandex.ru` для того аккаунта, куда активируем, и запускаем:
```
ya make && ./get_oauth_code auth --sessionid='3:abcefg...'
```

Из ответа сохраняем `OAuth token` и `uid`, их и используем в `am start`

## Отладка DIV2JSON

Для отладки div json вам надо иметь установленную утилиту jq

Linux
```
sudo apt install jq
```

MacOS
```
brew install jq
```

Далее надо иметь девайс подключенным по adb (можно проверить ```adb devices -l```) и дальше можно пользоваться такой командной строкой

```
$A/smart_devices/android/script/centaur.sh execute show_view ~/w.json
```

Где

* $A - корень аркадии
* execute - команда
* show_view - директива
* ~/w.json - путь до файла json с содержимым директивы (со структурой ```{"layer": {"content":{}}, "div2_card": {"body": {{"card": {"log_id": "AA"}, "templates": {}}}}```)
