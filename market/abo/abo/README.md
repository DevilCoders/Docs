
ABO
===

Служба Контроля Качества Яндекс.Маркета.


Cборка
------
```
# configure idea
# BASIC: ya idea -r ~/workspace/abo --yt-store
# GUIDE: https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi-tools/arcadia
ya-idea

# run local
java DebugMain
```

АБО будет считать, что вы залогинены под юзером с соответствующими правами исходя из пропертей
см. debug.user.uid, debug.user.actions

### Деплой на дев-сервер

```
# upload to dev
ssh-agent && ssh-add
ya package abo-main
./upload-to-dev.sh
```

Liquibase
---------
```
./libuibase-dev.sh updateSQL
```

Команды:
- `update` - применить
- `updateSQL` - посмотреть применение
- `changelogSync` - обновить мета-данные без применения ченж-сетов
- `changelogSyncSQL` - тоже самое, без реальных изменений

Окружения:
- `dev`
- `testing`
- `production`


Checkstyle
----------
Локально проверить [инструкция MBO](https://wiki.yandex-team.ru/users/padme/mboCheckStyle/)
Быстро починить `@SuppressWarnings("all")`



Деплой в тестинг из бранча
----------
см upload-to-dev


Java-Sec
----------
Настраивается через csv-файл.

https://a.yandex-team.ru/arc/trunk/arcadia/market/abo/abo/abo-java-sec-csv

### Раскатить в тестинг
https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/java-sec/java-sec-migrator/migration.sh

### Выполнить download.sh перед запуском тестов из IDEA

[File link](../download.sh)

[Arcadia link](https://a.yandex-team.ru/arc_vcs/market/abo/abo/download.sh)
