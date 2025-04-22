# Используемые технологии
## a.yaml

Основной файл проекта. Используется для описания владельца, merge требований, а так же CI сборки.

### Ссылки

[Анонс кабинета проекта](https://clubs.at.yandex-team.ru/arcadia/24868)

[Директивы a.yaml](https://wiki.yandex-team.ru/a.yaml/)

[Мерж-требования](https://docs.yandex-team.ru/arcanum/pr/merge-reqs)

[Проект maps mobile](https://a.yandex-team.ru/projects/maps-core-mobile-arcadia-ci/code/maps/mobile?dir=maps%2Fmobile)

[Конфиг для maps/mobile `maps/mobile/a.yaml`](https://a.yandex-team.ru/arc_vcs/maps/mobile/a.yaml)

[Конфиг для бинаризированных sandbox задач: `maps/mobile/sandbox/a.yaml`](https://a.yandex-team.ru/arc_vcs/maps/mobile/sandbox/a.yaml)

## CI
### Ссылки

[Документация по CI](https://docs.yandex-team.ru/ci/)

[YAML anchors](https://support.atlassian.com/bitbucket-cloud/docs/yaml-anchors/)

[Поля в переменной `context` (класс `TaskletContext`)](https://a.yandex-team.ru/arc_vcs/ci/tasklet/common/proto/service.proto)

[Поля для sandbox resource](https://a.yandex-team.ru/arc_vcs/ci/tasklet/common/proto/sandbox.proto)

 [Задачи: `ci/registry/projects/maps/mobile/`](https://a.yandex-team.ru/arc_vcs/ci/registry/projects/maps/mobile)


### Как тестировать {#testing-with-ci}

CI умеет запускать actions в прекоммитных проверках с учетом изменений в `a.yaml` и в задачах в `ci/registry`. Так что основным способом тестирования является создание ревью с нужными изменениями. Если измененный/новый flow не запускается в прекоммитных проверках, то можно временно добавить action с запуском в pr, протестировать и удалить его перед коммитом.

## TEAMCITY_SANDBOX_RUNNER

Набор sandbox задач, предназначенный для сборки iOS и android приложений. Через конфиг настраивается требование к окружению. Сама сборка описывается bash командами.

{% note info %}

Задачи изначально созданы для запуска из teamcity, отсюда и название. Но, фактически, это полностью sandbox задачи и teamcity в них никак не используется.

{% endnote %}

### Ссылки

[Документация](https://docs.yandex-team.ru/teamcity-sandbox-runner/)

[Конфиги: `maps/mobile/ci/tsr`](https://a.yandex-team.ru/arc_vcs/maps/mobile/ci/tsr)

[Примеры запуска](https://sandbox.yandex-team.ru/tasks?children=true&type=TEAMCITY_SANDBOX_RUNNER_LAUNCHER&author=robot-mapkit-ci&limit=20)

### Как тестировать
#### Изолированно

Для запуска сборки используется sandbox задача `TEAMCITY_SANDBOX_RUNNER_LAUNCHER`.
Задача поддерживает передачу конфига как через файл (параметр `config_path`), так и текстом через параметр `config`. Для тестирования через файл можно закоммитить новый конфиг к себе в `junk`.

{% note warning %}

В TSR есть баги, из-за которых конфиг, переданный через  `config` и тот же конфиг, переданный через файл, могут по-разному работать. Перед коммитом стоит проверить работоспособность конфига, переданного через файл

{% endnote %}

#### В CI flow

[См. CI](#testing-with-ci)

## YT кэш

Сборочный кэш, хранящийся в YT. Используется для ускорения как сборки в CI (TestEnv), так и локальной сборки.

### Ссылки

[Документация](https://docs.yandex-team.ru/ya-make/usage/ya_make/yt_store)

[Выделенный YT кэш](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/mobile/build_cache) ([Legacy путь](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps_mobile_build_cache))

[Графики YT кэша](https://solomon.yandex-team.ru/?b=365d&project=yt&service=accounts&dashboard=yt-account-limits-media&account=maps_mobile_build_cache&cluster=hahn)

[Шедулер YT_CACHE_CLEANER](https://sandbox.yandex-team.ru/scheduler/698102/view)

[Шедулер YT_CACHE_CLEANER для удаления висячих ссылок](https://sandbox.yandex-team.ru/scheduler/712957/view)

[Настройки для использования в CI](https://a.yandex-team.ru/arc_vcs/maps/mobile/a.yaml?rev=da6917cdf146f1db982257fb62174ab452abdc68#L26)


## Sandbox
### Ссылки

[Документация](https://docs.yandex-team.ru/sandbox/)

[Бинаризация задач](https://docs.yandex-team.ru/sandbox/dev/binary-task)

[Обычные (небинарные) задачи:`sandbox/projects/maps/mobile`](https://a.yandex-team.ru/arc_vcs/sandbox/projects/maps/mobile)

[Бинарные задачи:`maps/mobile/sandbox`](https://a.yandex-team.ru/arc_vcs/maps/mobile/sandbox)

[Статистика использования апи](https://grafana.yandex-team.ru/d/000016022/sandbox-api-stats-for-user-production?orgId=1&from=now-6h&to=now&var-user=robot-mapkit-ci&var-quota_owner=MAPS-CORE-MOBILE-CI)

### Как тестировать бинарные задачи

{% note alert %}

Собирать задачи нужно на linux

{% endnote %}

#### Изолированно

1. Собрать: `ya make --checkout -r`
2. Запустить: `./<Task> run --create-only --enable-taskbox`. В результате будет создан draft задачи в sandbox

Если параметры задачи не поменялись, то можно:
1. Собрать: `ya make --checkout -r`
2. Загрузить в sandbox: `./<Task> upload --enable-taskbox`
3. В sandbox склонировать предыдущий запуск и в **Advanced** поменять `Tasks resource` на новый

#### В CI flow

1. Собрать: `ya make --checkout -r`
2. Загрузить в sandbox: `./<Task> upload --enable-taskbox`
3. Прописать новый resource id в соответствующей CI  задаче (`ci/registry/projects/maps/mobile/`). Добавить pr action по необходимости ([См. CI](#testing-with-ci))
4. Создать ревью

## Тасклеты
### Ссылки

[Описание](https://wiki.yandex-team.ru/sandbox/tasklets/)

[Сборка](https://docs.yandex-team.ru/ya-make/manual/project_specific/tasklet)

[Как писать для CI](https://docs.yandex-team.ru/ci/job-tasklet)

### Как тестировать

{% note alert %}

Собирать задачи нужно на linux

{% endnote %}

#### Локально

1. Собрать: `ya make --checkout -r`
2. Запустить: `./<Task> run --local --input 'входные данные в формате json' <Task>`. Задача будет запущена как обычная программа

#### Изолированно в sandbox

1. Собрать: `ya make --checkout -r`
2. Запустить: `./<Task> run --sandbox-tasklet --input 'входные данные в формате json' <Task>`

#### В CI flow

1. Собрать: `ya make --checkout -r`
2. Загрузить в sandbox: `./<Task> sb-upload --sb-schema`
3. Прописать новый resource id в соответствующей CI  задаче (`ci/registry/projects/maps/mobile/`). Добавить pr action по необходимости ([См. CI](#testing-with-ci))
4. Создать ревью

## Solomon и Monitoring

**Solomon** - система мониторинга с визуализацией метрик (временных рядов) и возможностью алертинга. Не умеет логировать одиночные события и связанные с ними метаинформацию, только статистическая информация.
**Monitoring** - новый UI для Solomon. Использует те же данные, но пока умеет только отображать метрики.

CI сам отгружает в Solomon информацию о статусах всех задач.

### Ссылки

[Алерты в Solomon](https://solomon.yandex-team.ru/admin/projects/mapkit-in-ci/alerts)

[Проект в Monitoring](https://monitoring.yandex-team.ru/projects/mapkit-in-ci)

[Дашборд](https://monitoring.yandex-team.ru/projects/mapkit-in-ci/dashboards/mon4o4rurnha99cbqrdu?from=now-1d&to=now&refresh=60000)

### Как тестировать alert-ы

Нужные селекторы для алерта можно подобрать [на этой странице](https://solomon.yandex-team.ru/?project=ci-metrics&cluster=stable&service=processes&abc=maps-core-mobile-arcadia-ci). Там же, нажав на Graph, можно увидеть получившийся график.

После сохранения алерта, если он должен сработать, придет сообщение по выбранным каналам.

## Testenv [Legacy]
### Ссылки

[Документация](https://wiki.yandex-team.ru/testenvironment/)

[Проект maps-mobile](https://beta-testenv.yandex-team.ru/project/maps-mobile/timeline)

[TestEnv задачи](https://a.yandex-team.ru/arc_vcs/testenv/jobs/maps_mobile)
