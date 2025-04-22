# О сборке и деплое проекта
В этой доке собрана информацию о сборке Авто.ру. Дока призвана дополнить понимание разработчиков и тестировщиков о том, как собираются отдельные части проекта, а также прояснить детали, связаные с нашей технической инфраструктурой. Веб Авто.ру состоит из нескольких очень похожих друг на друга приложений (с точки зрения сборки и деплоя), поэтому тут будут рассматриваться аспекты сборки и деплоя фронтовых приложений вообще.

## Сборка в TeamCity
Как это обычно бывает, ответы на многие жизненные вопросы или по крайней мере подсказки можно найти в логах. Чтобы Build Log в [TeamCity](https://t.vertis.yandex-team.ru) читался легче, нужно немного погрузиться в суть происходящего в TeamCity.

### Основные термины
Проект — набор билд-конфигураций. Сборки пакетов, скриншотные тесты, и проч. В нашем случае это [`Auto.ru Frontend Repo`](https://t.vertis.yandex-team.ru/project/vs_frontend_Applications_AuroRuFrontendRepo?mode=builds).

Агент — железная тачка, сконфигурированная под запуск билд-конфигов TeamCity.

Билд-конфиг — набор пошаговых инструкций для агента, в результате запуска которого мы получаем что-то, в нашем случае это собранное приложение или отчет о запуске тестов. Например [`Vertis Frontend Release Shiva`](https://t.vertis.yandex-team.ru/admin/editBuildRunners.html?id=template:vs_frontend_Applications_VertisFrontendReleaseShiva), от которого с небольшими изменениями отнаследованы все сборки приложений фронта Авто.ру.

Билд — процесс сборки по описанному билд-конфигурейшну. Также используется в смысле конечный output/артефакт сборки — докер-образ (Docker image), из которого поднимаются контейнеры на серверах, для тестов это будет аллюр-отчет и папка с проблемными скриншотами.

### Сборка
Агент чекаутит указанную ветку.
Начинает выполнять шаги (build steps) из билд-конфига (см. [базовый конфиг](https://t.vertis.yandex-team.ru/admin/editBuildRunners.html?id=template:vs_frontend_Applications_VertisFrontendReleaseShiva)). Каждый шаг имеет свою конфигурацию и запускает определенный набор команд на агенте: `make deps`, `make build` и проч. Так собираются наши приложения:

* `build`:
Запускает сборку проекта (команды `make ...`). Транспилируется код, собираются бандлы. Подробнее в разделе про `make build`.

* `deploy static to S3`:
Деплоит статику в S3. Под статикой здесь подразумевается все, что насобирал Webpack: бандлы, стили, и прочие ассеты. Как они раскладываются на S3? Они лежат в куче, в названии присутствует хеш, соответствующий его содержанию (что по сути есть версия), так что если содержимое файла не изменилось, он остается в кеше браузера. У каждого приложения есть `HTML.js`, где описывается, как статика попадает в HTML на сервере. `HTML.js` читает `stats-client.json` собирает урлы статичных файлов, добавляет на страницу нужные теги: `script`, `link` и другие.

* `prepare docker container build`:
Готовит сборку докер-образа (Docker image), в основном просто перемещает папки.

* `build docker container`:
Запускает скрипт [`docker-autorelease`](https://a.yandex-team.ru/arcadia/classifieds/infra/vertis-packages/yandex-vertis-autorelease/data/usr/bin/docker-autorelease), который собирает докер-образ и пушит его в [общеяндексовый Docker registry](https://wiki.yandex-team.ru/docker-registry/), а также пушит в Git-репу релизный тег. В образе содержится наше серверное приложение, которое на виртуалке мы собираем и запускаем командой make, а на боевой тачке из образа поднимается контейнер в котором запускается приложение.

* `report status`:
Пишет результат работы сборки в Build Log.

## Команды make
Если кто не знает, `make` это утилита для кастомных компиляций и сборок, хотя этим использование не ограничивается. Если интересно поковыряться в мейкфайлах, стоит сначала пробежаться глазами по доке (хотя бы первые глав 5): https://www.gnu.org/software/make/manual/html_node/index.html. Синтаксис мейкфайлов не очевидный, но достаточно минут 10 повтыкать в документацию и сам файл, чтобы начать видеть в нем какие-то смыслы. На Хабре есть какие-то тьюториалы, написанные на родном языке, ссылаться на это тут не будем.

Немного о важных частях сборки.

### make deps
Устанавливает зависимости (`npm ci`) и генерит типы из про протобаф-схеме из schema-registry (`make protobuf-ts`).

### make protobuf-ts
Кажется это важно упомянуть. На всякий случай оставлю здесь эту доку: https://a.yandex-team.ru/arcadia/classifieds/autoru-frontend/docs/protobuf.md.

### make build
Выбираются конфиги, собираются JS-бандлы для сервера и для клиента, собирается сервер (`build-ts`), сохраняется слепок бункера (`bunker-cache`).

## Другие аспекты сборки и деплоя
Кроме работы TeamCity, есть еще пара моментов, которые нужно знать.

### nginx
Продовые конфиги `nginx` хранятся отдельно в репе [vertis-packages](https://a.yandex-team.ru/arcadia/classifieds/infra/vertis-packages/yandex-vertis-config-nginx-front/src/etc/nginx/sites-enabled), а дев-конфиги лежат в нашей репе в папке `/dev-configs`.

### Шива (новая админка admin.yandex-team.ru)
Если сборка в TeamCity прошла успешно, релиз или кастомная сборка (бранч) попадают в Шиву (скрипт `docker-autorelease` дергает соответствующую ручку). Шива сразу раскатывает релиз в тестинг. Дальше из Шивы релиз можно раскатить на канарейку и на прод.

Из-за ограничения на имя (до 24 символов) все сервисы называются `af-<название>`.

* [af-desktop](https://a.yandex-team.ru/arcadia/classifieds/services/maps/af-desktop.yml)
* [af-desktop-bem](https://a.yandex-team.ru/arcadia/classifieds/services/maps/af-desktop-bem.yml)
* [af-cabinet](https://a.yandex-team.ru/arcadia/classifieds/services/maps/af-cabinet.yml)
* [af-desktop-compare](https://a.yandex-team.ru/arcadia/classifieds/services/maps/af-desktop-compare.yml)
* [af-desktop-reviews](https://a.yandex-team.ru/arcadia/classifieds/services/maps/af-desktop-reviews.yml)
* [af-embed](https://a.yandex-team.ru/arcadia/classifieds/services/maps/af-embed.yml)
* [af-forms](https://a.yandex-team.ru/arcadia/classifieds/services/maps/af-forms.yml)
* [af-mag](https://a.yandex-team.ru/arcadia/classifieds/services/maps/af-mag.yml)
* [af-mobile](https://a.yandex-team.ru/arcadia/classifieds/services/maps/af-mobile.yml)
* [af-mobile-compare](https://a.yandex-team.ru/arcadia/classifieds/services/maps/af-mobile-compare.yml)
* [af-mobile-reviews](https://a.yandex-team.ru/arcadia/classifieds/services/maps/af-mobile-reviews.yml)
* [af-poffer](https://a.yandex-team.ru/arcadia/classifieds/services/maps/af-poffer.yml)
* [af-printer](https://a.yandex-team.ru/arcadia/classifieds/services/maps/af-printer.yml)
* [af-search-app](https://a.yandex-team.ru/arcadia/classifieds/services/maps/af-search-app.yml)

Полная документация лежит у админов в вики https://wiki.yandex-team.ru/vertis-admin/deploy/.

Важные моменты:
* мета-информация про проект описывается в https://a.yandex-team.ru/arcadia/classifieds/services;
* текущий статус можно узнать у [бота](https://t.me/vertis_shiva_bot) или в номаде ([тестинг](https://nomad.test.vertis.yandex.net), [прод](https://nomad.vertis.yandex.net));
* собранный контейнер автоматически выкатывается в тестинг;
* в прод надо выкатывать через [бота](https://t.me/vertis_shiva_bot) или [админку](https://admin.vertis.yandex-team.ru/);
* логи можно смотреть в [Grafana Explore](https://grafana.vertis.yandex-team.ru/explore), выбрав вверху `vertis-logs`. Подробнее про логи в [документации админов](https://docs.yandex-team.ru/classifieds-infra/logs/quick-start#chtenie).

### Кондуктор
Через кондуктор на железные сервера выкатываются:
* [autoru-frontend-parsing](https://c.yandex-team.ru/packages/autoru-frontend-parsing).

Если пакета в списке выше нет, его можно найти в поиске по кондуктору: https://search.yandex-team.ru/csearch?text=autoru-frontend-&.

### Секреты
Все секреты доставляются в проект в виде переменных окружения. Сами секреты мы храним в [Секретнице](https://yav.yandex-team.ru/). У каждого приложения есть файл `secrets.config.json`, в котором записаны секреты в формате `ID СЕКРЕТА:ID ВЕРСИИ:КЛЮЧ` (искать в поиске можно по id секрета). `secrets.config.json` используются только для дева, где виртуалка через пакетик `@vertis/secrets-to-dotenv` забирает секреты. В тесте/проде в переменные окружения секреты доставляет Шива. Список продовых секретов лежит в репе https://a.yandex-team.ru/arcadia/classifieds/services/, где лежат декларации приложений для Шивы.

### Статика
Репа со статикой — https://a.yandex-team.ru/arcadia/classifieds/yandex-vertis-autoru-static. Там лежат `robots.txt`, фавиконки, и прочее нужное для разных доменов Вертикалей. Собирается отдельной джобой в TC и деплоится через Кондуктор. В README.md написано всё, что надо знать для использования. Может деплоиться разработчиком без особых приготовлений.

А еще есть [MDS S3](https://a.yandex-team.ru/arcadia/classifieds/autoru-frontend/docs/mds-s3.md).
