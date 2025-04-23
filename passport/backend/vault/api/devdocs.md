# Заметки для разработчиков Секретницы

## Компоненты

Разрабатываем Секретницу в Аркадии. Для сборки используем Сендбокс и утилиту [passport/ci](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/ci). Для конфигурирования демонов [passport/configurator](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/configurator)

* АПИ Секретницы — [passport/backend/vault/api](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault/api)
* Документация — [passport/backend/vault/docs](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault/docs)
* Библиотека для Питона — [library/python/vault_client](https://a.yandex-team.ru/arc/trunk/arcadia/library/python/vault_client)
* Библиотека для Го — [library/go/yandex/yav](https://a.yandex-team.ru/arc/trunk/arcadia/library/go/yandex/yav)
* Утилита yav — [passport/backend/cli/yav](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault/cli/yav)
* Утилита yav-deploy — [passport/backend/cli/yav_deploy](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault/cli/yav_deploy)
* Общие библиотеки для клиента и АПИ — [passport/backend/vault/utils](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault/utils)

## Релиз АПИ

Исправляем версию АПИ в файле [passport/backend/vault/api/configs/base.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault/api/configs/base.yaml?rev=6857806#L25) ключем application.version. Версия из этого файла показывается в документации и используется, чтобы определить надо ли депрекейтить версии питонячьего клиента и консольных утилит.

Собираем утилитой passport/ci из папки [passport/backend/vault/api/deb](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault/api/deb). Утилите тоже даем команду поднять версию.

Дальше собирается по стандартному процессу: комит в Аркадию, тикет, таска в Сендбокс, таска в кондуктор.

Если добавляем хосты в тестинг или прод, то не забываем добавить их в соответствующий конфиг с окружением в [passport/backend/vault/api/configs](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault/api/configs), ключ application.hosts. Хосты для Zookeeper лежат в ключе ylock.hosts.

## Релиз документации

Документация релизится вместе с АПИ. Как поменять доку описано ниже.

Документация состоит из двух частей:
* статической в файле [passport/backend/vault/docs/src/App.vue](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault/docs/src/App.vue)
* динамической из ручки [/1/docs/](https://vault-api.passport.yandex.net/1/docs/). Описание ручек парсим из докстрингов к классам ручек.

Если меняли только описание ручек в py-файлах, то достаточно перевыкатить АПИ.

Если меняли файл App.vue, то надо пересобрать документацию скриптом [passport/backend/vault/docs/build.sh](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault/docs/build.sh). Скрипту нужна NodeJS и он пытается установить все зависимости самостоятельно. Иногда приходится запускать «с толкача» — не всегда удается с первого раза подкачать все зависимости.

Когда сборки комитим новые js- и map- файлы из [passport/backend/vault/docs/dist/static/js](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault/docs/dist/static/js) и не забываем удалить арком старые. Выкатываем релиз АПИ.

## Релиз Клиента

Клиент состоит из двух частей: библиотека для Питона и консольные утилиты yav (ya vault)/yav-deploy. Утилиты выкатывам deb-пакетом, библиотеку пакетом в PyPi.

Перед релизом меняем версию клиента в файле [library/python/vault_client/vault_client/__init__.py](https://a.yandex-team.ru/arc/trunk/arcadia/library/python/vault_client/vault_client/__init__.py).

Собираем deb-пакет из папки [passport/backend/vault/cli/deb](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault/cli/deb) утилитой passport/ci. На клиент в кондукторе подписаны многие проекты, поэтому катим в два этапа. Сначала выкатываем в тестинг, если через 1-2 дня нет жалоб от проектов, то катим в стейбл (без престейбла) хотфиксом.

Собираем и выкатываем PyPi пакет таской BUILD_VAULT_CLIENT_PYPI в Сендбоксе. Пример — [https://sandbox.yandex-team.ru/task/616973792/view](https://sandbox.yandex-team.ru/task/616973792/view)

Код задачи сборки PyPi-пакета в Сендбоксе — [sandbox/projects/passport/build_vault_client_pypi](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/passport/build_vault_client_pypi)

Чтобы обновить ya vault не делаем ничего — автоматика девтулзов сама через день-два соберет новую версию при очередной пересборке утилиты ya.

## Клиентские библиотеки

Библиотека для Питона изначально была клиентом для тестов АПИ Секретницы, но потом стала отдельным проектом. Поэтому клиент состоит из двух частей — публичной и закрытой.

Публичная лежит в [library/python/vault_client](https://a.yandex-team.ru/arc/trunk/arcadia/library/python/vault_client), закрытая в [passport/backend/vault/api/test/test_vault_client.py](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault/api/test/test_vault_client.py). Если мы делаем новую публичную ручку, то добавляем метод в открытый клиент, если ручка нужна только нам (например, фронтенду, админам и т.п.), то оставляем метод в закрытой части. Вместе с питоновской библиотекой лежит минимальный набор тестов. Основные тесты клиента — это тесты АПИ и консольных утилит.

От питоновской библиотеки зависит напрямую и транзитивно куча проектов в Аркадии, поэтому есть неприятный сайд-эффект от изменений в коде клиентской библиотеки. В PR пролезают флапающие тесты из совершенно незнакомых мест Аркадии. В таких случаях мы глазами просматривали поломавшиеся тесты и если не видили криминала, то вливали PR, проигнорировав ошибки в тестах неизвестных нам проектов. :)

Го-клиент поддерживает Го-комитет. Мы только ревьюим изменения. Го клиент поддерживает очень ограниченный набор методов АПИ.

## Как задепрекейтить старых клиентов

Питоновская библиотека и утилиты yav/yav-deploy ходят в ручку АПИ /status/, чтобы проверить версию клиента. Ручка возвращает булево поле is_deprecated_client. Если поле равно false, то клиенты выдают предупреждение про старую версию и предлагают обновить клиент.

Предупреждать про старых клиентов имеет смысл, если в утилиты yav/yav-deploy внесены существенные изменения и, обязательно, когда меняем алгоритм ssh-подписи для запросов к АПИ.

Минимальную версию клиентов меняем в файле [passport/backend/vault/api/configs/base.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault/api/configs/base.yaml) в ключе application.deprecated_before_version и перевыкатываем АПИ.

## Тесты

Тесты АПИ и утилиты yav сделаны вокруг АПИ. Т.е. мы не мокаем АПИ, а запускаем его для каждого теста, заполняем дынные через клиента и тестируем ответы ручек. В yav-deploy используется две ручки Секретницы и они замоканы.

Для тестов вместо MySQL используем Sqlite. SQLAlchemy помогает не сильно беспокоится о различии в базах. Для полнотекстового поиска, который существенно различается в майсиквеле и эскулайте тестов не делали — проверяли поиск руками.

## База данных

В базе нигде не используем автоинкрементные поля. Целочисленные ключи приезжают только из других баз (Стаф, АБЦ), В таблицах Секретницы используется монотонно-возрастающий уникальный идентификатор — [ULID](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/utils/ulid.py). Улиды храним в базе в поле char (с кодировкой). Мы в коде конвертируем идентификаторы в нижний регистр, поэтому можно перейти на поле binary, если будет проблемы с производительностью поиска по первичным ключам.

База нешардированная. Варианты шардирования обсуждали в [VAULT-26](https://st.yandex-team.ru/VAULT-26).

## Миграции БД

Смотри [migrations/README.md](migrations/README.md)

Миграции никогда не катим Питоном. Всегда гененируем SQL-скрипт и катим руками админов. Аккуратно меняем текущие таблицы — пользуйтесь атомарным DDL в MySQL.

## Переход на третий Питон

Эксперимент по переходу делали в [VAULT-808](https://st.yandex-team.ru/VAULT-808). В тикете есть patch-файл.

Каких-то существенных затыков при переходе на PY3 нет. Возня будет в двух местах. Обычная пляска с кодировками и различием байтовых строк при переходе с двойки на тройку. Вторая проблема специфична для Секретницы: мы используем функции map/filter/reduce, а в третьем питоне они возвращают итераторы. Поэтому len(filter) прийдется менять на len(list(filter)) и map на list(map) во многих местах.

yav-deploy тестируется под обеими версиями Питона. В релиз пока обираем под PY2.

## Запуск dev-сервера

При локально разработке иногда требуется запустить АПИ. Dev-сервер запустится на Sqlite.

* Переходим в папку passport/backend/vault/api/bin
* ya make
* ./vault_api db upgrade
* ./vault_api download staff; ./vault_api download abc; ./vault_api download tvm_apps
* ./vault_api run

В АПИ проще всего ходить через yav: `YAV_BACKEND="https://localhost:9500" yav list secrets`

Стадии апгрейда базы и загрузки кешей Стафа/АБЦ/ТВМ можно пропустить, если мы ничего не меняли в базе или у нас уже есть база с кешами и нам не нужны новые данные для тестов.

## Автор документа

Олег Волчков<br/>
mailto: oleg@volchkov.net<br/>
Telegram: [Unhandled_Exception](https://t.me/Unhandled_Exception)<br/>

Пока я под NDA, готов ответить на вопросы. :)
