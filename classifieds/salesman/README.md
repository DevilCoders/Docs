# Salesman

Salesman - сервис, ответственный за платные услуги на auto.ru.

## salesman-api

HTTP API, с которым работают только дилеры.

[Swagger](http://salesman-api-http-api.vrts-slb.test.vertis.yandex.net/swagger/) (testing)

## salesman-user-api

HTTP API, с которым работают только обычные пользователи(частники).

[Swagger](http://salesman-user-api-http-api.vrts-slb.test.vertis.yandex.net/swagger/) (testing)

## salesman-tasks

Фоновые процессы, связанные с дилерами.

[Swagger](http://salesman-tasks-scheduler-api.vrts-slb.test.vertis.yandex.net/swagger/) (testing)

## salesman-user-tasks

Фоновые процессы, связанные с частниками.

## Запустить сервис на dev машине, доступной по ssh

1. Найдите папку сервиса, который вы хотите запусить удаленно.
2. Положите в поддиректорию assembly **upload.properties** файл следующего содержания:

```properties
ssh.host=ваш_хост
ssh.username=ваш_логин
```

3. Запустите соответствующую **deploy-xxx** инструкцию makefile'a. Пример:

```bash
make deploy-salesman-api
```

# Релиз пакетов

Общая информация:

1. В названии ветки и PR нужно указывать ID тикета на st. Если хочется в название ветки добавить ещё небольшое словесное
   описание, отделить его от ID тикета знаком подчёркивания. Например: `AUTORUOFFICE-4865_release_improvements`. Если
   отделять дефисом или каким-либо другим символом, шива при выкладке может не распарсить ID тикета в комментарии к
   тикету, и не прикрепить выкладку к тикету.
2. В комментарии к commit-у, нужно указывать тикет на st. Это нужно для автоматической сборки манифеста изменений.
3. Вручную коммитить changelog не нужно. Джобы TeamCity сами изменяют changelog локально в процессе билда, затем
   запускают скрипт autorelease, деплоящий пакет. Джобы не коммитят changelog в репозиторий.

## Релиз в тестинг

* Сделать PR с нужной ветки
* Запустить в TeamCity общую
  сборку [release all packages](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_Salesman_SalesmanShivaRelease_ReleaseAllPackages?mode=builds)
  , указав нужную ветку. Ветка имеет вид "users/robot-stark/classifieds/salesman/2709728/head". Можно собрать только
  нужные пакеты, запустив соответствующие сборки. После сборки пакеты выкатятся в соответсвующий бранч в шиве. Чтобы
  поставить эту версию на основной тестинг, нужно будет запустить деплой в админке с указанием нужной версии.

Версия пакетов со своей ветки будет такой `X.Y.pull-2489257-<commit hash>`

## Релиз в продакшн

1. Смержить свою ветку в trunk.
2. Запустить
   джоб [release all packages](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_Salesman_SalesmanShivaRelease_ReleaseAllPackages?mode=builds)
   , не указывая отдельную ветку. По умолчанию подставляется trunk. Номер версии пакетов: `X.Y.r<arcadia revision>`.
   После сборки, пакеты автоматические зальются на тестинг. В тикеты шивы джоб подставляет номера тикетов st, собирая их
   из разницы между версией в stable и тем, что собралось из trunk.
3. Выкатить новые пакеты в [шиве](https://admin.vertis.yandex-team.ru/services). Джоб выкатывает стабильный релиз только
   в тестинг. Для каждого тикета в релизе должна быть ссылка на выкладку в прод. Проще всего это сделать, добавив ключи
   тикетов в комментарий к выкладке в шиве.

# Интеграция c IntelliJ IDEA:

1. Скопируйте файлы из **./idea_build_configurations** в **.idea/runConfigurations**
2. Теперь вы можете запускать некоторые конфигурации из IDEA.

# Форматирование кода

В этом проекте используется [scalafmt](https://scalameta.org/scalafmt/) для форматирования кода. Для того чтобы
отформатировать весь код, необходимо запустить:

```
make fmt
```

Таким образом запускается форматирование всех файлов, изменённых относительно мастера. На случай проблем, можно
запустить форматирование абсолютно всех файлов (оно обычно сильно дольше):

```
make full-fmt
```

# Написание тестов

Весь код, находящийся в /main для шаринга между тестами в разных модулях, должен быть в пакете `ru.auto.salesman.test`.
Это необходимо для упрощения игнорирования такого кода в местах, где мы хотим посчитать метрики продакшн-кода: например,
test coverage.

Тесты с promocoder могут не работать на маке, но должны работать в удалённых TC билдах.

# Фичи

Логику, которую хочется менять в рантайме без деплоя, можно заворачивать в фичу. На данный момент фичи есть только для
дилеров, т.к.:

1. Прямо сейчас они требуются только для дилеров.

Для дилерских сервисов salesman-api и salesman-tasks свои общие фичи. Для сервисов частников salesman-user-api и
salesman-user-tasks также свои общие фичи.

Пример получения списка фичей с их значениями:
`curl -H 'Content-Type: application/json' 'http://$hostname:1030/api/1.x/service/autoru/features'`

Пример обновления значения фичи:
`curl -X PUT -H 'Content-Type: application/json' 'http://$hostname:1030/api/1.x/service/autoru/features/call-placement' -d 'true''`
где call-placement -- имя фичи, true -- новое значение фичи (передаётся в теле запроса).

После такого обновления в коде, в котором используется эта фича, её значение станет `true`.

Фичи хранятся в ZooKeeper. При инициализации сервисов, если не удалось создать клиент ZooKeeper для работы с фичами,
зажигается мониторинг. Также производится фоллбек, чтобы не ронять весь сервис:

1. В salesman-tasks все значения фич считаются дефолтными (initialValue).
2. В salesman-api все ручки для работы с фичами пятисотят.

# Конфигурация

Конфиги - это постоянные фичи. Используются для временного включения-выключения каких-то вещей, служебные.

На данный момент в системе используются следующие конфигурационные флаги:

* `salesman`
    * `is-salesman-cashback-signals-enabled` - включает-выключает обработку очереди кешбеков из кафки.
    * `is-moderation-updates-for-dealers_autoru-enabled` - включает-выключает обработку очереди дилерских резолюций из
      кафки.
* `salesman-user`
    * `user-quota-passport-events` - включает-выключает обработку очереди сообщений из кафки паспорта.

в случае, если требуется передвинуть оффсеты очереди, конфиг надо выключить, потом включить обратно

Пример получения списка конфигов с их значениями:
`curl -X GET --header 'Accept: application/json' 'http://$hostname:$port/api/1.x/service/autoru/configurations`

Пример обновления значения конфигов:
`curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'X-Salesman-User: 11111' -d 'false' 'http://localhost:1030/api/1.x/service/autoru/configurations/$configName'
`
где

* $configName -- имя конфига
* false -- новое значение конфига (передаётся в теле запроса)
* $port
    * 1030 для `salesman`
    * 1050 для `salesman-user`

После такого обновления в коде, в котором используется данный конфиг, его значение станет `false`.

Конфиги хранятся и настраиваются аналогично фичам (единственное отличие - они предполагаются постоянными и не будут
выпиливаться)

# Документация

* [Основной раздел на вики](https://wiki.yandex-team.ru/vertis/autoru-money-dev/)
* [Code Style Guide](https://wiki.yandex-team.ru/vertis/autoru-money-dev/Code-Style-Guide/)
* [Полезные ссылки](https://wiki.yandex-team.ru/vertis/autoru-money-dev/links/)

# Базы данных

База salesman-user живёт в MDB.

* [Тестинг](https://yc.yandex-team.ru/folders/foo2qvhfq9b2r709olo5/managed-mysql/cluster/mdbgg0190u76kuok4tpm)
* [Креденшалы для подключения к тестингу](https://github.com/YandexClassifieds/datasources/blob/fb4d24f094b86b5434c6d865b0540c379435be58/roles/vertis-datasources/templates/testing.conf.j2#L1830-L1835)
* [Прод](https://yc.yandex-team.ru/folders/foo2qvhfq9b2r709olo5/managed-mysql/cluster/mdbf70tqn8iop2hf3mqh)
