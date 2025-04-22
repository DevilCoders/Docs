# DMP (репликация)

Выгрузки в YT осуществляются [сервисом репликации](https://wiki.yandex-team.ru/taxi/backend/architecture/replication/) на платформе [DMP](https://wiki.yandex-team.ru/dmp/platform/dmpsuite/) (кратко ознакомиться с платформой можно посмотрев [видео](https://wiki.yandex-team.ru/dmp/platform/prezi/#2020-08-25rasskazprodmpdljarazrabotkiedy)). Сервис репликации, опираясь на [правила репликации](https://github.yandex-team.ru/taxi-dwh/dwh/tree/develop/replication_rules), копирует данные из таблиц БД в YT по заданному расписанию. Вместо реальных таблиц выгружаются представления `*_dmp_view`. Это избавляет от написания подготавливающего данные кода для выгрузки по API (такая возможность также есть в сервисе репликации).

## Настройка выгрузки из БД в YT

### Подготовка инфраструктуры

Если для сервиса ещё ни разу не создавались репликации, то надо добавить секрет с подключением к БД в [конфигурацию сервиса replication-tasks](https://tariff-editor.taxi.yandex-team.ru/services/38/edit/174/secrets).

У каждого набора правил должна быть указана команда ответственных. Нужно убедиться что команда есть в [конфиге DEV_TEAMS](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/DEV_TEAMS). Если команды нет, то нужно прописать её и запросить права на ОКи драфтов [по инструкции](https://docs.yandex-team.ru/taxi-replication/docs/arcadia/responsible#otvetstvennost-za-pravila-replikacii).

### Подготовка окружения

Для удобства разработки и тестирования можно воспользоваться виртуалкой

Создать и настроить виртуалку: https://wiki.yandex-team.ru/dmp/platform/dmpsuite/getting-started/dev-on-vm

Когда дойдешь до пункта конфигурации CTL в папке arcadia/taxi/dmp/dwh/config/local, то содержимое файлов ctl.yaml и pgaas.yaml, актуальных для нашего проекта, можно посмотреть в [секретнице](https://yav.yandex-team.ru/secret/sec-01g7egpbkr6f5mc0f18aadhq0a/explore/version/ver-01g7eh5dyegk5hn6h91sg451s1).

<details>
    <summary> Необязательные пункты
(удобно для локальной разработки, но съест кучу времени и не критично, можно сразу переходить к след пункту)</summary>
    Поднять сервис репликации на виртуалке: https://wiki.yandex-team.ru/users/desire/remotepycharm/#nastrojjkareplikacii. Проще всего поставить debian-пакет, но для прогона тестов потребуется сам код. Важно настроить запуск: https://wiki.yandex-team.ru/users/desire/remotepycharm/#lokalnyjjzapusk.

    Чтобы код автоматически попадал на виртуалку при написании можно установить и настроить PyCharm: https://wiki.yandex-team.ru/dmp/platform/dmpsuite/getting-started/pycharm
</details>

### Разработка

В простых случаях следует воспользоваться [скриптом генерации правил](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/dmp/dwh/replication_rules#генерация-правил). Сгенерированные правила можно дорабатывать вручную. Можно запустить скрипт прямо на виртуалке либо через удаленное выполнение через PyCharm (нужно находиться в директории с правилами репликации).

__Если__ в твоей въюхе есть jsonb поля, то перед запуском команды ниже лучше сразу сходить в [конфиг](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/dmp/dwh/replication_rules/rules_generator/config.yaml) и поправить строчку в struct_yt_cast с ```any: 'to_yson_safely_extended'``` на ```any: jsonb_string_to_yson```. Без этого в YT колонки с jsonb будут просто строкой с экранированными кавычками.

Команда для генерации правил выгрузки таблиц БД в YT:
```
taxi-python3 rules_generator --source postgres \
                             --tables <таблицы *_dmp_view на тестинге через пробел> \
                             --scope pigeon
                             --yt-struct --primary-keys id
                             --secret-source POSTGRES_LAVKA_PIGEON
```

Скрипт сгенерирует описание источника репликации (БД), описание типов данных в YT, описание мапперов и тесты к ним в директории с назвнаием сервиса. Дальнейшие правки вносятся в соответствие с [описанным форматом](https://docs.yandex-team.ru/taxi-replication/docs/arcadia/how_to_start#rule). В частности, вручную прописывается крон/период запусков.

Если требуется поменять формат сгенерированных полей, но не хочется вручную вносить правки в мапперы и тесты к ним, можно перед запуском генерации поменять [конфигурацию](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/dmp/dwh/replication_rules/rules_generator/config.yaml) `struct_yt_types_map` и `struct_yt_cast`.

### Тестирование

(Все, что ниже, актуально только если ты заморочился и настроил полное локальное окружение для разработки. Если же ты этого не сделал, то переходи к следующему пункту и тестируй сразу на тестинге)

Для проверки работы правил генерации можно запустить репликацию на виртуалке:
```
DMP_INSTALL_DIR=/path/to/dwh/replication_rules \
REPLICATION_LOCAL_PATH=/path/to/replication.local.yaml \
    yandex-taxi-replication-local run <название сервиса>_<название таблицы>
```
После успешного завершения появится таблица на YT в директории `replica/postgres/<service>/<table>` с префиксом, указанном в replication.local.yaml.

Запуск тестов при наличии склонированного репозитория backend-py3 можно выполнить на виртуалке командой:
```
BACKEND_PY3=BACKEND_PY3=/path/to/backend-py3 make test make test
```

### Релиз

Если результат выгрузки устраивает, то нужно созадть PR, пройти ревью и выкатиться в тестинг. Выкатка пускается [здесь](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_DMP_ReplicationRules_Customs_CustomTesting?mode=builds#all-projects)
Через какое-то время после выкатки в тестинг в [админке](https://tariff-editor.taxi.tst.yandex-team.ru/replications) появятся правила репликации.
Все правила будут в состоянии неинициализированных. Для инициализации нужно изменить состояние всех правил на init, создать драфт и аппрувнуть его. Подробнее в [документации](https://docs.yandex-team.ru/taxi-replication/docs/arcadia/drafts).

После инициализации в YT появятся пустые таблицы (пустые при выгрузке снапшотами и частично заполненные при инкрементальной выгрузке) в директории //home/lavka/testing/replica/postgres/<service>.
Подробнее в документации https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/replication-docs/replication-service/#_7
Вручную запустить таски нельзя, нужно дождаться когда они выполнятся кроном в указанное в конфиге время. После выполнения таблицы заполнятся данными.

После проверки данных в тестинге мержим ПР и проделываем шаги по выкатке и инициализации тасок в проде.
Релизы прода живут [здесь](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_DMP_ReplicationRules_Releases_AutoRelease?mode=builds#all-projects). Ребята вроде часто катают релизы (минимум раз в день на июль 2022) и проще не катить самому и возиться с оками, а подождать чужого релиза, который заберет твои изменения.
Админка прода живет [здесь](https://tariff-editor.taxi.yandex-team.ru/replications).
В остальном действуем как на тестинге.

### Алерты

Чтобы заработали алерты, надо сделать PR в репозиторий infra-cfg-juggler [по инструкции](https://docs.yandex-team.ru/taxi-replication/docs/arcadia/responsible#otvetstvennost-za-pravila-replikacii).
Алерты на конкретный скоуп правил не поддерживаются, но под каждый скоуп можно завести свою команду ответственных в DEV_TEAMS.
Ответственных в самом конфиге джаглера можно указать в формате `'@svc_<service>:duty-<service>'`.
Пример: https://github.yandex-team.ru/taxi/infra-cfg-juggler/pull/4987/files
