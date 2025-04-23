### Базовый образ для фронтовых проектов в QYP

#### Использование
1. Найти последний запуск [по фильтру](https://sandbox.yandex-team.ru/tasks?tags=QEMU_IMAGE%2CMETRIKA_FRONTEND&type=BUILD_PORTO_LAYER&all_tags=true&limit=20)
2. Использовать `rbtorrent:` ресурс при создании виртуалки
3. При первом логине запустить скрипт `source setup_frontend_environment` для настройки окружения

#### Сборка и выкладка новых версий образа
1. Склонировать последнюю задачу из пункта 1
2. Поставить ей теги `QEMU_IMAGE` и `METRIKA_FRONTEND`
3. После сборки зайти в ресурс с типом `QEMU_IMAGE_SEARCH_BIONIC_DEVEL` и проставить ему `Important`

Это приведет к проставлению атрибута ttl (time to live) в значение inf и ресурс не будет удален через 14 дней [скрин](https://jing.yandex-team.ru/files/rifler/2021-06-15_00-25-22.png)
