Automation service Arbitrage-CGI
==========================

[Подробная документация тут](https://wiki.yandex-team.ru/taxi/arbitrage-cgi)

### Локальный деплой

Чтобы запустить сервлет локально необходимо преднастроить параметры окружения и среду.
Во-первых, прямо с проектом поставляются конфиги запуска (run-configs). Чтобы они работали и подхватывались — нужна свежая версия IntelliJ IDEA 2020.2. После импорта проекта достаточно открыть меню конфигураций запуска и там появятся все нужные конфиги.

Для запуска понадобится заиметь рабочий и поднятый инстанс PostgreSQL. Установить на мак можно так: `brew install postgresql`. Завести database и юзера с именем `postgres` и таким же паролем. Базу пристегнуть на 5432 порт (по-умолчанию на нём и запускается). Дальше всё само — в ран-конфиге уже прописаны пути к базе и таблицы там создадутся автоматически.

Поскольку сервис активно ходит за ключами доступа в Секретницу, локально мы подменяем их. В частности, чтобы использовать тестовые данные и окружение, а не ходить в прод.

1. В модуле `mock-vault-io` создаём файл `src/tokens.kt`
2. Описываем в этом файле простую структуру:
```kotlin
val keyValueStub = listOf(
    VersionValue("abc-service", "3017"),
    //...
)
```
Она будет необходима, когда сервис начнёт спрашивать у замоканной Секретницы всевозможные ключи. 

[Полный список продовых ключей можно найти здесь](https://yav.yandex-team.ru/secret/sec-01dbzgct6x8mx4zx7sxm8rzj0b/) (доступ есть не у всех, если вам он очень нужен — пишите в личку).
Если доступов у вас нет, можно взять ключи из докерфайла ([Dockerfile.backend](./Dockerfile.backend), сразу после блока RUN идёт блок ключей для Секретницы), а значения добыть самостоятельно, авторизовавшись в соответствующих сервисах.
Пример персонального мока (вместо каналов в телеге — личный чатик с роботом):
```kotlin
val keyValueStub = listOf(
    VersionValue("abc-service", "3017"),
    VersionValue("bb-oauth", "AQAD-*"),
    VersionValue("email-password", "*"),
    VersionValue("email-username", "robot-taxi-mob-infra"),
    VersionValue("github-cookie", "*"),
    VersionValue("github-oauth", "*"),
    VersionValue("staff-oauth", "AQAD-*"),
    VersionValue("startrek-oauth", "AQAD-*"),
    VersionValue("taxi-dev-client-chat-id", "68491337"),
    VersionValue("taximeter-dev-client-chat-id", "68491337"),
    VersionValue("taxi-client-testing-chat-id", "68491337"),
    VersionValue("taximeter-testing-chat-id", "68491337"),
    VersionValue("telegram-admin-chat-id", "68491337"),
    VersionValue("telegram-news-inform-chat-ids", "68491337"),
    VersionValue("telegram-bot-token", "*"),
    VersionValue("upsource-oauth", "Basic *"),
    VersionValue("head-testing-department", "106249"),
    VersionValue("taxi-duty-oauth", "AQAD-*"),
    VersionValue("duty-taximeter-groups", "5e3bec2da387bee45c99f551,5e3bec23a387bee45e99f551,5d516466a387bed0dc226189,5c8ba50f8ef826648b945d69,5ca72eaaa387be93dd9f24b1,5c4ed938398be3fb4cb0971f"),
    VersionValue("yql-oauth-token", "AQAD-*"),
    VersionValue("clickhouse-auth-token", "basic#login#pass")
)
```
Если какой-то функционал не используется, то в качестве пароля/токена можно использовать любую заглушку от балды. До тех пор, пока это позволяет вам запускать полноценно сервис и тестировать нужный функционал :)
Если будут проблемы — приходите в личку, поможем.

3. После этого запускаем конфиг `Run mock-vault`
4. Следом `Run arbitrage-app`
5. Опционально, `Run frontend`

Поскольку модуль мока Секретницы является сервлетом, его нельзя встроить в пайп для запуска сервиса одной кнопкой, увы.

Чтобы потестить крон-скрипты, нужно в файле gradle.properties подставить правильный путь к локальной папке со скриптами. Вместо `cgi.cron.directory=cronscripts` написать: `cgi.cron.directory=Users/$username/IdeaProjects/TaxiArbitrage/cronscripts` (!!без слэша в начале!!).
Быстро взять путь к папке проекта можно консольной командой: `pwd | pbcopy` (для мака, или `pwd | xclip` для линукса).

Аналогично чтобы потестить скрипты в метрику, нужно в файле gradle.properties подставить правильный путь к локальной папке со скриптами. Подменив `cgi.metrics.scripts.directory`.

#### Известные траблы при сборке/деплое

1. После `clean` сборка бэкенда собирается со второго раза — из-за бага компилятора Котлина :(
2. Сборка может падать со странными ошибками в кэшах компилятора — помогает `clean`. Почему-то ломается МПП.
3. Иногда `mock-vault-io` отдаёт некорректную строку на запрос из сервиса. Помогает повторить запрос (сам сервис падать не должен).
4. Если стреляет на бэкенде ошибка `PKIX path building failed`, то устанавливаем сертификат по инструкции: https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vjava

#### Локальная отладка в Docker Compose

Сперва определиться, какие контейнеры нужно собрать локально, а какие можно взять готовые.  
В файле `docker-compose.debug.yml` можно добавить указатель версии для образов, вместо `latest` указав `${VERSION}` (и значение этого аргумента надо будет передать при запуске оркестратора).  

0. Собираем в докер-образ микросервис для раздачи секретов: `./gradlew :mock-vault-io:docker` (компиляция уже связана с таской докера)  
1. Собираем в докер-образ основной бэкенд Арбитража: `./gradlew :backendJarWithCodegen :docker`  
2. Запускаем оркестратор конфигом `Run orchestra` или из консоли командой: `VERSION=1.0.0-rc54 docker-compose -f docker-compose.debug.yml up -d --force-recreate`  
3. Чтобы остановить оркестрацию, просто стопаем и клацаем андеплой (если запускали конфигом), или в консоли вызываем: `docker-compose down --remove-orphans`  
4. Параметр `VERSION=1.0.0-rc54` указывает, какую базовую версию выкачать из сети (для базы данных и фронтенда), можно не указывать, если собираете все контейнеры локально из исходников.  
5. Чтобы собрать все контейнеры локально, в файле `gradle.properties` укажите параметр `cgi.arbitrage.version=latest`, затем запустите конфиги `Dockerize pgsql` и `Dockerize frontend`.