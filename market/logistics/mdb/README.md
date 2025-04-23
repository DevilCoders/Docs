# Market delivery bus
Приложение для обмена информацией между модулями Доставки и Маркета:
[https://wiki.yandex-team.ru/delivery/development/apps/mdb/](https://wiki.yandex-team.ru/delivery/development/apps/mdb/)

Флоу событий от Чекаутера (draw.io):
[https://drawio.yandex-team.ru/#LMDB%20event%20process%20flow.xml]()

## Local

1. Поднимаем докер контейнеры с моками необходимых сервисов [dependency-stubs](dependency-stubs/README.md).
   `cd 'dependency-stubs' && docker-compose up -d`.
2. Копируем стабовые проперти приложения.
   `cp mdb-app/src/main/properties.d/local/application-local.properties.dist mdb-app/src/main/properties.d/local/application-local.properties`
3. Создаем Spring Boot Run Configuration c main классом
   `ru.yandex.market.delivery.mdbapp.MdbApplication` \
   (правой кнопкой на треугольник run рядом с классом `-> Modify Run Configuration`)
4. В созданной конфигурации проставляем Environment variables
   `LOG_DIR=logs;ENVIRONMENT=local;PROPERTIES_DIR=<абсолютный путь до директории src/main/properties.d>` и Working directory `$MODULE_WORKING_DIR$`
5. Далее стартуем приложение, которое начинает жить на порту прописанному тут `${http.port}`.
После этого можно начинать засылать запросы вида `curl localhost:{port}/ping`. Можно поправить настройки nginx в докере 
   и например  подложить нужное событие чекаутеру. 


## Про миграцию базы данных

Для создания файла миграции нужно создать новый файл миграции внутри `mdb-app/src/main/resources/db/changelog`

После чего конфигурим файл миграции в соответствии со своими нуждами, не забываем про строку rollback и
добавляем название файла в `mdb-app/src/main/resources/config/changelog.yml` по образу и подобию с другими файлами

чтобы миграция накатилась для локального запуска - делаем билд

## Запуск тестов

Юнит-тесты:
```
cd ~/arcadia/market/logistics/mdb/mdb-app/src/test
ya make -tt
```

Функциональные тесты:
```
cd ~/arcadia/market/logistics/mdb/mdb-app/src/integration-test
ya make -A
```

Все тесты:
```
cd ~/arcadia/market/logistics/mdb
ya make -A
```
