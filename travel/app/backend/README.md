# Бэкенд мобильного приложения

- код https://a.yandex-team.ru/arc_vcs/travel/app/backend
- deploy https://deploy.yandex-team.ru/projects/travel-app-backend
- CI https://a.yandex-team.ru/projects/travelapp/ci/releases/timeline?dir=travel%2Fapp%2Fbackend&id=regular-release
- wiki https://wiki.yandex-team.ru/travel/app/dev/

## Основное

Бэкенд - в основном, это прокси к другим сервисам.

На клиент отдаем только то, что нужно для отрисовки функционала. Потому что, все что, передадим на клиент, может быть
использовано правильно и не правильно, при этом по-своему на каждой из платформ. И версия мобильного приложения
выкаченая в стор, будет жить на устройствах, условно, вечно.

## Договоренности по взаимодействию

- [wiki](https://wiki.yandex-team.ru/travel/app/dev/#vzaimodejjstvieprilozhenijaibjekenda)
    - http, внутри proto. Потому что: proto - фиксирует контракт, и proto - меньше байтиков нужно переслать, актуально
      при плохом интернете, что для мобильного устройства не редкость
    - в тестинге/деве есть возможность использовать json вместо proto

## Технические детали

- grpc-gateway
    - возможность легко получить http с proto, и swagger

- API протокола мобильного приложения
    - proto складываем [сюда](https://a.yandex-team.ru/arc_vcs/travel/app/backend/api)
    - там же есть реадми с подробностями

- так как большая часть кода это проксирование запросов/ответов в другие бэкенды, то у нас много клиентов, их реализацию
  складываем [сюда](https://a.yandex-team.ru/arc_vcs/travel/app/backend/internal/lib)

## Тесты

Тесты пишем. Кроме очевидного, что тесты нужны, чтобы не сломать уже существующую функциональность, тесты помогут:

- понять что есть в ответе от другого бэкенда
- в случае бага, можно легко скопипастить существующий тест, и адаптировать его под конкретную ситуацию

- на клиенты пишем тесты, тогда по коду будет понятно, что приходит в ответе от другого бэкенда
- на хендлеры пишем тесты с моками клиентов

## Покрытие тестами

`./tools/run-cover.sh`

## Как запустить локально

1. Для локального запуска нужны определенные права, например, на получение секретов. Права есть у ABC Мобильного
   прилоения Путешествий, разработка.
2. Для запуска нужен TVM, чтобы он работал локально нужно
   установить [tvmtool](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#gdeskachatbinarnik)
3. Для mac установить md5sum `brew install md5sha1sum`
4. Запускаем приложение и TVM
    1. `./tools/run-dev.sh`
    2. с логированием запросов `./tools/run-dev-log.sh`

#### Дебаг в `GoLand`

1. Скачать справочники:
   `./tools/download-resources.sh`
2. `go install github.com/go-delve/delve/cmd/dlv@latest`
3. запускаем сборку для дебага `./tools/run-debug.sh`
4. `Run -> Attach to Process... -> .cmd/api/api`

## Swagger

При локальном запуске [dev url](http://localhost:8080/api/swagger/)

Для ручек требующих аторизацию важно, что адрес именно `localhost:8080`, потому что для этого адреса в тестовом паспорте
сделан колбэк TRAVELAPP-40 & OAUTHREG-459

Swagger бэкенда в [тестинге](https://app.testing.travel.yandex.net/api/swagger/)

**Важно**: при тестировании через сваггер злодейский хром подменяет user-agent на свой, даже если в сваггере указать
правильный. Из-за этого в хроме/ябро сваггер server-config всегда будет отдавать 400 с ошибкой, мол, неподдерживаемая
платформа. Бага эта именно в связке swagger + chromium, легко не поправить. Можно платформо-специфичные руки тестировать
из Safari, можно - из консоли, курлом)

## Форматирование кода, автоматическое создание ya.make для golang-кода

`./tools/fix-style.sh`

Обязательно запускаем перед отправкой ПР

## Серверный конфиг
Конфиг, который клиент применяет у себя, условно при старте приложения.
travel/app/backend/cfg/server_config.json
Распространяется в сборке с приложением, если какие-то элементы серверного конфига нужно править чаще/оперативнее чем
релиз, то выносим настройки в админку такси, в файле можем оставить дефолт.

## Конфиги из админки такси

Наше направление ```travel``` в адмминке:

- [тестинг](https://tariff-editor.taxi.tst.yandex-team.ru/experiments3/configs?removed=without_removed&enabled=all&active=all&is_technical=all&departments=travel)
- [продакшн](https://tariff-editor.taxi.yandex-team.ru/experiments3/configs?departments=travel&active=all&enabled=all&is_technical=all&removed=without_removed)

В деплое есть Workload exp3-matcher, актуальная версия exp3-matcher
прописана [тут](http://taxi/uservices/services/exp3-matcher/recipes/binary/recipe.ext), обновляем руками по мере
необходимости.

Для локализованных строк внутри конфига используем ключ в танкере вида ```tanker:<keyset>:<key>```,
например ```tanker:backend_config:update_available```.

#### Аргументы, которые передаем в такси

- ```application.platform``` - ios/android
- ```application.version``` - версия приложения вида 0.2.1
- ```application.version_code``` - версия int для android, например 4
- ```service``` - сервис travel-app-backend
- ```application``` - название приложения travelapp
- ```appmetrica_device_id``` - id, который выдает аппметрика для незалогинов
- ```passport_uid``` - паспортный uid залогина
- ```geo_id``` - geo_id пользователя получаем из геобазы
- ```region_geo_id``` - geo_id обобщенный до региона
- ```country_geo_id``` - geo_id обобщенный до страны
- ```locale.language``` - язык "ru" из локали "ru_US"
- ```locale.country_code``` - страна "US" из локали "ru_US"
