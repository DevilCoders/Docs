# auto.ru public api #

## Чаты ##

Общее обсуждение + саппорт: https://t.me/joinchat/BWIidg6ix2iTm27RylNJoA

Релизы: https://t.me/joinchat/BWIidkW5X09hKoVwipA_eA

## Адреса ##

Тестинг: http://autoru-api-server.vrts-slb.test.vertis.yandex.net/

Тестинг из бранчи: http://autoru-api-{branch}-server.vrts-slb.test.vertis.yandex.net

Продакшн: http://autoru-api-server.vrts-slb.prod.vertis.yandex.net/

Продакшн публичный: https://apiauto.ru/

## Логи ##
[grafana autoru-api](https://grafana.vertis.yandex-team.ru/explore?orgId=1&left=%5B%22now-1h%22,%22now%22,%22vertis-logs%22,%7B%22expr%22:%22service%3Dautoru-api%20%20layer%3Dtest%20%22,%22fields%22:%5B%22thread%22,%22context%22,%22message%22,%22rest%22%5D,%22limit%22:100%7D%5D)
## Документация ##

https://wiki.yandex-team.ru/autoru-dev/public-api/documentation/


## Разработка #

### code-style

В проекте используется scalafmt.

Есть плагин для idea: https://scalameta.org/scalafmt/docs/installation.html#intellij

#### Проверка стиля
~~~
make fmt-validate
~~~

#### Форматирование кода
~~~
make fmt
~~~

### Запуск тестов

При обычной разработке имеет смысл запускать только юнит тесты, они быстрее и не завязаны на сторонние сервисы.

Если вы пишете новые интеграционные тесты или ломаете логику старых, то вам необходимо:
1. Удалить папку `api-core/src/test/resources/integration/$testClassName`(только для существующих тестов)
2. Запустить интеграционные тесты в режиме записи
3. Закоммитить сгенерированные для тестов данные в репу вместе со своим pull request.

#### Только юнит тесты:
~~~
make unit
~~~

#### Интеграционные тесты

Работа с интеграционными тестами возможна в 4 режимах

1. Настоящие интеграционные тесты с реальными запросами в тестовые бекенды.
~~~
make integration-test
~~~
2. Запуск с предзаписанными ответами от бекендов(что технически делает их юнит тестами). Используется в обязательной проверке в pull request.
~~~
make integration-test-mocked
~~~
3. Генерация предзаписаных ответов для последующего использования в замоканных тестах. В этом варианте генерируются данные только для тех тестов, файлы которых отсутсвуют в `api-core/src/test/resources/integration`.
~~~
make integration-test-capture
~~~
4. Полная перегенерация всех mock данных. Не нужно использовать без крайней необходимости.
~~~
make integration-test-full-capture
~~~

Для управления режимами запуска отдельных тестов в idea нужно выставлять в конфигурации запуска переменную окружения MOCK_MODE:
- CAPTURE - принудительная запись
- SIMULATE - запуск с использованием mock-файлов
- SIMULATE_SOFT - SIMULATE, если mock-файлы существуют, иначе CAPTURE

#### Все тесты:
~~~
make test
~~~

### Локальный запуск

Настроить внешние ресурсы:
скачать файлы с DEV_HOST (виртуалки) через команды
```
scp DEV_HOST:/etc/yandex/vertis-datasources/datasources.json ~/ &&
scp DEV_HOST:/etc/yandex/vertis-datasources/datasources.conf ~/ &&
scp DEV_HOST:/etc/yandex/vertis-datasources/datasources.properties ~/
```
и положить эти три файла себе в `/etc/yandex/vertis-datasources/`

положить в `api-server/src/main/resources` `application.local.conf` из [секретницы](https://yav.yandex-team.ru/secret/sec-01fdh9xm77pc3rdfkkynqkqwf8)

Запустить в IDEA класс `ru.auto.api.Main`
Либо в консоли: `make start`

### Компиляция на удаленном сервере

Для ускорения времени компиляции и разгрузки ноутбука имеет смысл использовать компиляцию на удаленном сервере

Для этого необходимо один раз запустить `make init` для первичной настройки.

В дальнейшем большинство команд начнут исполняться на удаленном сервере:
~~~
make compile
make unit
make test
make deploy
~~~

Для выключения этой фичи следует удалить файл `scripts/mainframer.sh`

### Деплой на dev сервер

Поставить на машинку библиотеку `libticket_parser2`:
```
apt-get update
apt-get -y install libticket-parser2-java=2.2.3
```
Например, библиотека `libticket_parser2` есть в репозитории:

`deb http://yandex-vertis-xenial.dist.yandex.ru/yandex-vertis-xenial stable/amd64/`

Вписать адрес dev-машины в `upload.properties` в параметр `ssh.host`.
Пример: `ssh.host=my-dev-host.net`

Команда `make deploy` компилирует проект, заливает на сервер и перезапускает приложение.

Следы работы приложения можно найти в папке `~/dist/api-server/`на dev машине.

### Деплой в отдельный тестинг из ветки

Запустить [джобу](https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=VerticalsBackend_AutoruApi_Arcadia_MakeShivaRelease) на нужной ветке. Для pull request'а использовать ветку вида `users/robot-stark/classifieds/autoru-api/{номер PR}/head`.

После завершения выполнения найдите запущенный сервис [здесь](https://admin.vertis.yandex-team.ru/services/autoru-api). Название **ветки в Shiva** для pull request'а будет иметь вид `pull-{номер PR}`, для других случаев будет основано на имени ветки в Arc. Контейнер поднимется по адресу: `http://autoru-api-{ветка в Shiva}-server.vrts-slb.test.vertis.yandex.net`.

### CI

[Проект в Teamcity](https://t.vertis.yandex-team.ru/project.html?projectId=VerticalsBackend_AutoruApi)

Docker образ собирается после ручного запуска [джобы](https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=VerticalsBackend_AutoruApi_Arcadia_MakeShivaRelease)

Никаких changelog коммитить не надо.

### Shiva

[autoru-api](https://admin.vertis.yandex-team.ru/services/autoru-api)

### Выкладка в testing вручную
public-api можно задеплоить на  testing вручную, запустив сборку

"autoru-api" в

  https://admin.vertis.yandex-team.ru/services/autoru-api

с нужной версией и комментарием (иначе деплой упадет).
