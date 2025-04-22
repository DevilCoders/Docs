# Релизы через Sedem

![rolling](img/rolling.jpg "Катись!")

Sedem предоставляет следующий функционал для релизов:
- версионирует изменения и хранит [историю релизов](#release-history);
- осуществляет контроль за соблюдением [релизного цикла](#flow);
- предоставляет [информацию о состоянии](#release-info) сразу всех [деплой-юнитов](#glossary) сервиса;
- позволяет выкладывать изменения сразу в несколько [деплой-юнитов](#glossary), объединенных общим названием;
- отводит релизные ветки от транка и позволяет накатывать [хотфиксы](#release-hotfix) для релизов;
- создает [релизные тикеты](#glossary), куда добавляет [ченджлог](#changelog) для релиза и фиксирует все этапы деплоя;
- поддерживает [механизм двойных аппрувов](#sox) для sox-сервисов;
- поддерживает [автоматическое тестирование](#acceptance) сервисов.

На данный момент sedem умеет релизить:
- [nanny-сервисы](https://wiki.yandex-team.ru/runtime-cloud/nanny/);
- [огородные модули](https://docs.yandex-team.ru/garden/module-lifecycle#sedem);
- [sandbox-задачи](services/sandbox).

## Терминология { #glossary }

- релиз (`release`) - фиксированное состояние сервиса, привязанное к коммиту в Аркадии;
- версия релиза (`version`) - строка в формате `vX.Y`, состоит из мажорной и минорной частей;
- мажорный релиз (`major release`) - релиз c минорной версией равной 1, привязан к конкретной ревизии транка;
- релизная ветка (`branch`) - релизная арк-ветка, автоматически отводится от транка для каждого мажорного релиза;
- тэг релиза (`tag`) - маркер коммита в релизной ветке, соответствует минорной версии релиза;
- релизный тикет (`st-ticket`) - startrek-тикет в [очереди MAPSRELEASES](http://st.yandex-team.ru/MAPSRELEASES), соответствует мажорной версии релиза;
- хотфикс (`hotfix`) - релиз с минорной версией больше 1, привязан к коммиту в релизную ветку;
- деплой-юнит (`deploy-unit`) - независимая инсталляция сервиса (отдельный няня-сервис, контур модуля в огороде, sandbox-шедулер/шаблон);
- стейдж (`stage`) - набор деплой-юнитов, объединенных общей версией сервиса, всего стейджей 4: `unstable`, `testing`, `prestable`, `stable`;
- сборка (`build`) - sandbox-ресурс, который можно выкатить в деплой-юнит (докер-образ, огородный модуль, бинарник с sandbox-задачей);
- релиз-кандидат (`release candidate`) - транковая сборка, которому пока не соотвествует никакого релиза;
- деплой-кандидат (`deploy candidate`) - релиз, который пока не докатили до последнего стейджа (обычно `stable`);
- sox-сервис (`SOX`) - сервис, который требует [двойного аппрува](#sox) при выкладке в prestable и stable.

## Релизный цикл { #flow }

Sedem из коробки поддерживает следующий релизный цикл:
- на основе [заранее собранного](#autobuild) транковой сборки создается новый мажорный релиз командой [release start](#release-start);
- для мажорного релиза автоматика заводит релизный тикет и публикует в нем [ченджлог](#changelog);
- мажорный релиз сразу выкатывается в первый релизный стейдж (по умолчанию `testing`);
- релиз должен провести в стейдже не меньше времени, чем указано в конфиге сервиса;
- затем релиз можно выкатить в следующий стейдж командой [release step](#release-step);
- порядок прохождения стейджей фиксированный: `unstable` -> `testing` -> `prestable` -> `stable`;
- если у сервиса нет ни одного деплой-юнита в данном стейдже, то стейдж пропускается;
- цикл завершается, когда релиз оказывается в последнем стейдже (по умолчанию `stable`).

Кроме того, существует возможность:
- посмотреть [информацию о состоянии](#release-info) всех [деплой-юнитов](#glossary) сервиса;
- откатывать релизы через команду [release rollback](#release-rollback);
- создавать хотфиксы через [release hotfix](#release-hotfix);
- запускать сборку сервиса на любую транковую ревизию через [release build](#release-build);
- помечать релизы "бракованными" с помощью [release reject](#release-reject).

## Конфигурация сервиса { #deploy-setup }

Чтобы иметь возможность релизить сервис, нужно в `sedem_config` добавить поле `deploy.type` соответствующего типа:
- `rtc` - для няня-сервисов;
- `garden` - для огородных модулей;
- `sandbox` - для sandbox-задач;

и настроить [покоммитную сборку](#autobuild).

Например:

```yaml
# sedem_config/__all__.yaml

deploy:
    type: rtc
```

Полученный седем-конфиг надо закоммитить, после чего можно переходить к созданию конфига для покоммитной сборки.

{% note info %}

Вскоре после коммита ревью с конфигом седема на почту должна прийти отбивка со ссылкой на задачу, которая регистрирует сервисы.

Убедитесь, что задача завершилась успешно.

{% endnote %}

### Покоммитная сборка { #autobuild }

Для работы с релизами через Sedem необходимо сконфигурировать сборку для вашего сервиса по коммиту в Аркадию.

Для покоммитной сборки используется CI. [Документация по CI](https://docs.yandex-team.ru/ci/).

Для того, чтобы настроить сборку:

1. Запустите команду `sedem create_ci_config <path-to-service-dir>` в директории сервиса, чтобы получить `a.yaml`-конфиг.

    {% note alert %}

    Седем требует, чтобы `a.yaml` располагался строго рядом с седем-конфигом, а имя action'а, который триггерит флоу, было в точности `build`.

    {% endnote %}

2. В полученном конфиге необходимо указать uuid yav-секрета (`sec-XXX`) c oauth-токеном робота, от имени которого будет производиться сборка. Данный робот должен входить в [abc-сервис `maps-ci`](https://abc.yandex-team.ru/services/maps-ci). Подробнее о получении токена читайте в [документации CI](https://docs.yandex-team.ru/ci/quick-start-guide#get-token).

3. Для няня-сервисов необходимо дополнительно получить oauth-токен для работы с docker-registry и добавить его как `nanny_ci.token` в тот же yav-секрет, чей uuid указан в `a.yaml`. Получить токен для docker-registry можно, перейдя [по ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=34bd7c8cae1a417baa2d11bb0797a287) от имени робота.

    {% note warning %}

    Убедитесь в том, что у вашего робота есть доступ к секрету, где лежит его oauth. Т.е. робот должен смочь прочитать собственный токен из секретницы.

    Для этого нужно дать ему права на чтение секрета в yav. Если выдаете права на abc-сервис, то убедитесь, что у робота есть нужная роль в abc.

    {% endnote %}

    Кроме того, вы можете указать, кому нужно отправлять нотификации о результатах сборки. В качестве получателей поддерживаются логины конкретных сотрудников, адреса email-рассылок и sandbox-группы.

    {% note info %}

    По умолчанию конфиг устроен так, что CI будет запускать сборку на любой коммит в директорию сервиса. Чтобы изменить это поведение, отредактируйте [фильтры](https://docs.yandex-team.ru/ci/actions#filter) в конфиге.

    Кроме того, седем использует историю покоммитных запусков CI для того, чтобы добавлять [ченджлог](#changelog) изменений в стартрек-тикеты.

    Коммиты, для которых сборка была запущена вручную (по кнопке в CI), не попадают в ченджлог.

    {% endnote %}

4. Закоммитьте полученный конфиг (`a.yaml`) вместе с соответствующим sedem-конфигом (если не сделали это ранее).

5. Затем разрешите CI доступ к токену:
    - перейдите в [список проектов CI](https://a.yandex-team.ru/projects/all);
    - зайдите в свой проект (поиском по abc-сервису);
    - на вкладке `CI` (слева сбоку) зайдите в список action'ов;
    - выберите action, соответствующий ключу `build` в конфиге;
    - выдайте права на чтение секрета, который ранее вписали в конфиг (кнопка "Request token").

6. CI автоматически начнет сборку задачи на ревизии, в которой был добавлен `a.yaml`.

### Конфигурация релизного цикла { #deploy-config }

Релизный цикл описывается в sedem-конфиге сервиса:
```yaml
# sedem_config/__all__.yaml

deploy:
    deploy_profile: custom

deploy_profiles:
    custom:
        unstable:
            min_time: 0
            max_alert_history_window: 0
            targets: [unstable]
        testing:
            min_time: 30m
            max_alert_history_window: 1h
            targets: [testing, load]
        prestable:
            min_time: 24h
            max_alert_history_window: 1d
            targets: [prestable]
        stable:
            targets: [stable, datatesting]
```
В секции `deploy` указывается название профиля деплоя (по умолчанию `default`), а в секции `deploy_profiles` перечисляются сами профили. Каждый профиль описывает настройки стейджей, всего их 4: `unstable`, `testing`, `prestable` и `stable`. Каждый стейдж состоит из списка деплой-юнитов - независимых единиц деплоя (например, отдельных няня-сервисов), которые необходимо выкатывать одновременно.
Помимо списка деплой-юнитов профиль позволяет определить следующие настройки:
- `min_time` - минимальное время, которое релиз должен проверсти в текущем стейдже, прежде чем его можно будет катить дальше по релизному флоу;
- `max_alert_history_window` - максимальный размер временного окна [истории алертов, проверяемой перед релизом в следующий стейдж](#check-crits-before-deploy).

{% note warning %}

Также существует возможность переопределить релизный стейдж, с которого начинается релизный цикл - `initial_step_name`, однако делать это не рекомендуется.

{% endnote %}

Из коробки Sedem поставляется с профилями для всех типов сервисов, и их кастомизация нужна в редких случаях. Для изменения списка деплой-юнитов рекомендуется завести отдельный профиль вместо редактирования профиля по умолчанию.

{% note warning %}

Для sandbox-задач список деплой-юнитов формируется [автоматически на основании секции `resources`](services/sandbox#sedem-config).

{% endnote %}

Если хочется переопределить только некоторые параметры, то вместо создания кастомного профиля можно отредактировать дефолтный:
```yaml
# sedem_config/__all__.yaml

deploy_profiles:
    default:
        prestable:
            min_time: 1h
            max_alert_history_window: 30m
```

### Автоматическая выкладка сервиса

{% note warning %}

На текущий момент sedem не поддерживает автоматические релизы. Тикет: [GEOINFRA-1647](https://st.yandex-team.ru/GEOINFRA-1647).

{% endnote %}

## Поддерживаемые команды

`sedem release <command> <path-to-service>`

{% note info %}

`<path-to-service>` может быть как абсолютным путем в Аркадии, так и относительным текущей директории

{% endnote %}

```text
Commands:
  build        Run build task for specified revision.
  history      Show releases history.
  hotfix       Apply diff from specified commit to release...
  info         Show current deploy state and candidates.
  reject       Mark release as "rejected".
  rollback     Perform rollback for the specified stage.
  set-message  Attach message to the specified release.
  start        Create new release.
  step         Deploy release to the specified stage.
```

Для каждой конкретной команды можно посмотреть свой help: `sedem release <command> --help`

### release info

`sedem release info <path-to-service> [-r <releases-limit>] [-c <candidates-limit>] [--verbose] [--no-color] [--ascii-only]`

Команда `release info` выводит 3 таблицы:
- текущее состояние сервиса во всех [деплой-юнитах](#glossary);
- [кандидаты на деплой](#glossary);
- [кандидаты на создание релиза](#glossary).

{% note info %}

По умолчанию показывается не более 3-х кандидатов каждого типа. Максимальное кол-во кандидатов для отображения регулируется параметрами `-c|--candidates-limit` и `-r|--releases-limit`.

Более подробную выдачу можно получить, добавив флаг `-v|--verbose`.

{% endnote %}

```bash
$ sedem release info maps/infra/ecstatic/coordinator
Loading service state..............
┌ Service maps-core-ecstatic-coordinator ──────────────────┬─────────────────────────────────────────────────────────────────────┐
│             │ Released    │ Version  │ St ticket         │ Comment                                                             │
├─────────────┼─────────────┼──────────┼───────────────────┼─────────────────────────────────────────────────────────────────────┤
│ datatesting │ 2 weeks ago │ v82.1    │ MAPSRELEASES-7243 │ (@nikitonsky) ecsttc coordinator: add yasm connections count metric │
│      stable │ 2 weeks ago │ v82.1    │ MAPSRELEASES-7243 │ (@nikitonsky) ecsttc coordinator: add yasm connections count metric │
├─────────────┼─────────────┼──────────┼───────────────────┼─────────────────────────────────────────────────────────────────────┤
│   prestable │ 9 hours ago │ v84.1    │ MAPSRELEASES-7565 │ (@nikitonsky) Log while removing jams-speeds obsolete records       │
├─────────────┼─────────────┼──────────┼───────────────────┼─────────────────────────────────────────────────────────────────────┤
│        load │ a day ago   │ v84.1    │ MAPSRELEASES-7565 │ (@nikitonsky) Log while removing jams-speeds obsolete records       │
│     testing │ a day ago   │ v84.1    │ MAPSRELEASES-7565 │ (@nikitonsky) Log while removing jams-speeds obsolete records       │
├─────────────┼─────────────┼──────────┼───────────────────┼─────────────────────────────────────────────────────────────────────┤
│    unstable │ 3 hours ago │ r7900267 │ None              │ (@nikitonsky) Add empty group to ecstatic tests                     │
└─────────────┴─────────────┴──────────┴───────────────────┴─────────────────────────────────────────────────────────────────────┘
┌ Deploy (step) candidates ──────────────────┬───────────────────────────────────────────────────────────────┐
│   Version │ Created    │ St ticket         │ Comment                                                       │
├───────────┼────────────┼───────────────────┼───────────────────────────────────────────────────────────────┤
│     v84.1 │ a day ago  │ MAPSRELEASES-7565 │ (@nikitonsky) Log while removing jams-speeds obsolete records │
├───────────┼────────────┼───────────────────┼───────────────────────────────────────────────────────────────┤
│ [R] v83.1 │ a week ago │ MAPSRELEASES-7375 │ (@john-doe) Broken commit                                     │
└───────────┴────────────┴───────────────────┴───────────────────────────────────────────────────────────────┘
┌ Release (start) candidates ────────┬─────────────────────────────────────────────────────────────────────────────────┐
│  Version │ Created     │ Sb task   │ Comment                                                                         │
├──────────┼─────────────┼───────────┼─────────────────────────────────────────────────────────────────────────────────┤
│ r7900267 │ 3 hours ago │ 905712124 │ (@nikitonsky) Add empty group to ecstatic tests                                 │
├──────────┼─────────────┼───────────┼─────────────────────────────────────────────────────────────────────────────────┤
│ r7897762 │ a day ago   │ 904938103 │ (@chikunov) maps-yacare: add nginx server config for default vhost GEOINFRA-845 │
└──────────┴─────────────┴───────────┴─────────────────────────────────────────────────────────────────────────────────┘
```

Обозначения:
- цвета версий кандидатов обозначают статусы:
    - зеленый/без цвета - все ок, можно релизить;
    - желтый - в процессе подготовки (например, собирается);
    - красный - необратимая ошибка (например, сборка сломалась);
- пометка `[R]`/`[REJECTED]` - релиз помечен как ["rejected"](#release-reject);
- цвет версий деплой-юнитов меняется на красный, если все версии в рамках одного стейджа не совпадают;
- цвет даты релиза деплой-юнита меняется на красный/голубой, если версия меньше/больше стейбла соответственно;
- цвет даты релиза деплой-юнита становится красным, если этот релиз не докатили до стейбла за необходимое время (сейчас неделя).

### release history

`sedem release history <path-to-service> [-l <branches-limit>] [--no-pager] [--no-color]`

Команда `release history` выводит историю релизов в хронологическом порядке.

{% note info %}

По умолчанию показываются только последние 5 релизов. Кол-во релизов для отображения регулируется параметром `-l|--limit`.

{% endnote %}

```bash
$ sedem release history maps/infra/teaspoon -l 3
Loading service state..............
Release v5.2 (load, testing)
Source commit: https://a.yandex-team.ru/arc/commit/7442057
Target commit: https://a.yandex-team.ru/arc_vcs/commit/0474134af4722d37072382f9f509c7ea7acbeb7f
Build task: https://sandbox.yandex-team.ru/task/790309945
St ticket: https://st.yandex-team.ru/MAPSRELEASES-4838
Released to: testing
Created at: 20:14 06 Oct 2020
Comment: (@alexlmikh) OTT-13718 [ott-api/karate] Fixture cleanup [strong:all]

Release v5.1 (stable)
Commit: https://a.yandex-team.ru/commit/7440737
Build task: https://sandbox.yandex-team.ru/task/790088559
St ticket: https://st.yandex-team.ru/MAPSRELEASES-4838
Released to: testing, stable
Created at: 20:12 06 Oct 2020
Comment: (@robot-maps-sandbox) Update base image version: stable to 7415115

Release v4.5 [REJECTED] [BUILD DELETED]
Source commit: https://a.yandex-team.ru/arc_vcs/commit/bb95bdc7493db7eb8b22f37d120b08c2a43eb4f1
Target commit: https://a.yandex-team.ru/arc_vcs/commit/6b184969fa9b6b1c2442beaec4a9053cd2e13aa3
Build task: https://sandbox.yandex-team.ru/task/790304496
St ticket: https://st.yandex-team.ru/MAPSRELEASES-4723
Released to: -
Created at: 20:05 06 Oct 2020
Comment: (@vmazaev) remove newline
```

{% note info %}

Для отображения используется pager `less` (если не переопределен через переменную деплой-юнита окружения `PAGER`), который запустит режим паджинации, если вывод не влезает на 1 экран терминала.
Использование пейджера можно принудительно отключить параметром `-P|--no-pager`.

{% endnote %}

### release start

`sedem release start <path-to-service> [<revision>] [-m <message>]`

Команда `release start` создаст новый релиз и сразу же запустит его деплой в [первый релизный стейдж](#flow).
Создание релиза включает в себя:
- отведение [релизной ветки](#glossary) от выбранной транковой ревизии;
- заведение [релизного тикета](#glossary);
- сборка [ченджлога](#changelog).

Ревизию для релиза рекомендуется выбрать из списка доступных релизных кандидатов в списке [release info](#release-info).
Можно не указывать конкретную ревизию, тогда будет выбран самый новый кандидат из списка.

{% note warning %}

Если нужной ревизии в списке кандидатов нет:
- проверьте, хватает ли вам лимита `-c|--candidates-limit` для отображения всех кандидатов;
- если была зарелижена более новая ревизия, то ваш коммит уже вошёл в неё;
- в противном случае воспользуйтесь командой [release build](#release-build), чтобы собрать нужную ревизию и получить кандидата на релиз (не лишним будет также проверить настройки [покоммитной сборки](#autobuild)).

{% endnote %}

{% note info %}

При создании релиза можно указать [кастомное описание](#release-set-message) через флаг `-m|--message`

{% endnote %}

```bash
$ sedem release start maps/infra/teaspoon
Loading service state............
Looking for sandbox build resource...
Found resource #1997197085 (r7865833)
Will deploy r7865833 to "testing": (@robot-maps-sandbox) Update base image version: to 7847239
Proceed to deploy? [y/N]: y
Creating new release version...
Created release v18.1
Starting deploy to testing...
Started deploy of release v18.1 for maps-core-teaspoon to testing
```

### release step

`sedem release step <path-to-service> <version> <stage>`

Команда `release step` проверяет необходимые условия и запускает выкладку релиза в выбранный [релизный стейдж](#glossary).
Список проверяемых условий:
- релиз не был помечен как ["rejected"](#release-reject);
- выбранный релизный стейдж соответствует [последовательности деплоя](#flow);
- релиз провел [минимально необходимое время](#flow) в предыдущем релизном стейдже;
- нет горящих мониторингов в предыдущем релизном стейдже.

Версию релиза рекомендуется выбирать из списка кандидатов на деплой в выдаче команды [release info](#release-info).

{% note warning %}

Если нужного релиза в списке кандидатов нет:
- проверьте, хватает ли вам лимита `-r|--releases-limit` для отображения всех кандидатов;
- если вы пытаетесь откатить версию релиза, воспользуйтесь командой [release rollback](#release-rollback) и выберите версию из списка, предоставляемого этой командой;
- в противном случае ваш сценарий не стандартный, воспользуйтесь командой [release history](#release-history), чтобы получить полный список релизов.

{% endnote %}

```bash
$ sedem release step maps/infra/teaspoon v18.1 prestable
Loading service state............
Looking for release...
Found v18.1 (r7865833 / sbr #1997197085)
Will deploy v18.1 (r7865833) to "prestable": (@robot-maps-sandbox) Update base image version: to 7847239
Proceed to deploy? [y/N]: y
Starting deploy to prestable...
Started deploy of release v18.1 for maps-core-teaspoon to prestable
Post notifying in ST ticket MAPSRELEASES-7655 ...
```

### release build

`sedem release build <path-to-service> [<revision>]`

Команда `release build` запускает сборку для выбранной ревизии и возвращает ссылку на CI.
Как только таска создаст sandbox-ресурс, ревизия появится в списке кандидатов команды [release info](#release-info).

Если не указать ревизию, будет собран самый свежий транк.
Если указать ревизию svn-ветки вместо ревизии транка, команда завершится ошибкой.

```bash
$ sedem release build maps/infra/sedem/sandbox/dummy_task r8877914
Will build r8877914: (@ladunoff) [ydo_backend] parse minimal_cost == "" hotfix
Proceed to build? [y/N]: y
Build started: https://a.yandex-team.ru/projects/maps-core-sedem-machine/ci/actions/launch?dir=maps/infra/sedem/sandbox/dummy_task&id=build&number=22
```

### release hotfix

`sedem release hotfix <path-to-service> -b <branch> (-r <revision>|-a <arc-hash>)`

Команда `release hotfix`:
- скопирует переданный коммит в релизную ветку,
- создаст релиз с новой минорной версией,
- запустит его сборку.

Если все прошло успешно, то когда сборка завершится, хотфикс можно катить, как и любой другой релиз:
- через тестинг (рекомендуемый способ): `sedem release step <path-to-service> <hotfix-version> testing`;
- сразу в (pre-)stable с явным подтверждением из-за нарушения порядка:
`sedem release step <path-to-service> <hotfix-version> (prestable|stable)`.

В качестве версии релиза нужно указывать только мажорную версию.
Передавать коммит можно как по ревизии, если это транк, так и по арк-хэшу, если это арк-ветка.
При этом коммиты из svn-веток **не поддерживаются**, хотя у них имеется ревизия.

{% note warning %}

Каждый следующий хотфикс применяется поверх текущего состояния релизной ветки, т.е. содержит все изменения, внесенные предыдущими хотфиксами, в т.ч. может их частично или полностью откатывать.

Если при попытке применить хотфикс происходит **merge-conflict**, то изменения не применяются, и вам нужно самостоятельно [влить их в ветку](#merge_conflict).

Одному хотфиксу соответствует ровно один коммит, поэтому если вы хотите влить сразу несколько коммитов, вам нужно самостоятельно [объединить их в один](#commits_squash).

{% endnote %}

```bash
$ sedem release hotfix maps/infra/teaspoon -b v17 -r r7833697
Release v17.3 (r7833697) for maps-core-teaspoon is merging
(repeat the same command to check for updates)
```

{% note info %}

Можно выполнить команду несколько раз или воспользоваться [release info](#release-info) для отслеживания статуса релиза.

{% endnote %}

```bash
$ sedem release hotfix maps/infra/teaspoon -b v17 -r r7833697
Release v17.3 (r7833697) for maps-core-teaspoon is building
Hotfix task [READY]: https://sandbox.yandex-team.ru/task/907449268
Build task [RUNNING]: https://sandbox.yandex-team.ru/task/907449841
(repeat the same command to check for updates)
```

#### Разрешение merge-конфликтов { #merge_conflict }

Если у вас произошел **merge-конфликт**, выполните следующие команды, чтобы самостоятельно влить коммит в ветку и разрешить конфликт:
- загрузите состояние релизной ветки с сервера арка: `arc fetch releases/maps/<service-name>-<major-version>`, например, `arc fetch releases/maps/core-teapot-42`;
- отведите свою ветку от релизной: `arc co -b <user-branch-name> releases/maps/<service-name>-<major-version>`, имя вашей ветки может быть любым;
- примените коммит, который хотите влить в релизную ветку: `arc cherry-pick r<commit>`, и разрешите конфликт;
- скопируйте хэш полученного коммита;
- запуште состояние вашей ветки на сервер арка: `arc push --set-upstream users/<username>/<user-branch-name>`;
- выполните команду `sedem release hotfix -b <major-version> -a <commit>` с полученным арк-хэшом коммита.

#### Объединение нескольких коммитов в один хотфикс { #commits_squash }

Если вы хотите объединить несколько коммитов в один хотфикс:
- загрузите состояние релизной ветки с сервера арка: `arc fetch releases/maps/<service-name>-<major-version>`, например, `arc fetch releases/maps/core-teapot-42`;
- отведите свою ветку от релизной: `arc co -b <user-branch-name> releases/maps/<service-name>-<major-version>`, имя вашей ветки может быть любым;
- выполните команду `arc cherry-pick <commit-1> <commit-2>...`;
- выполните команду `arc rebase -i trunk` и объедините нужные коммиты в один (`squash`);
- скопируйте хэш полученного коммита;
- запуште состояние вашей ветки на сервер арка: `arc push --set-upstream users/<username>/<user-branch-name>`;
- выполните команду `sedem release hotfix -b <major-version> -a <commit>` с полученным арк-хэшом коммита.

### release rollback

`sedem release rollback <path-to-service> <stage> [<version>]`

Команда `release rollback` откатит выбранный стейдж **на указанную** версию.

Если не указать версию, команда вернет список кандидатов на роллбек.

```bash
$ sedem release rollback maps/infra/teaspoon testing v17.1
Loading service state............
Looking for release...
Found v17.1 (r7833696 / sbr #1974305353)
Will deploy v17.1 (r7833696) to "testing": (@robot-metrika-test) Update tasks/__init__.py
Proceed to deploy? [y/N]: y
Starting deploy to testing...
Started deploy of release v17.1 for maps-core-teaspoon in testing
Post notifying in ST ticket MAPSRELEASES-7159 ...
```

```bash
$ sedem release rollback maps/infra/teaspoon testing
Loading service state............
Target release version is not specified for rollback
(use "sedem release rollback <path> testing <version>" to make rollback)
┌ Testing releases for maps-core-teaspoon (among last 10) ──────────────────────────────────────────────────────────┐
│ Version │ Released    │ St ticket         │ Comment                                                               │
├─────────┼─────────────┼───────────────────┼───────────────────────────────────────────────────────────────────────┤
│   v18.1 │ 2 hours ago │ MAPSRELEASES-7655 │ (@robot-maps-sandbox) Update base image version: to 7847239           │
├─────────┼─────────────┼───────────────────┼───────────────────────────────────────────────────────────────────────┤
│   v17.1 │ 3 weeks ago │ MAPSRELEASES-7159 │ (@robot-metrika-test) Update tasks/__init__.py                        │
├─────────┼─────────────┼───────────────────┼───────────────────────────────────────────────────────────────────────┤
│   v16.1 │ 3 weeks ago │ MAPSRELEASES-7080 │ (@robot-maps-sandbox) Update base image version: to 7788225           │
├─────────┼─────────────┼───────────────────┼───────────────────────────────────────────────────────────────────────┤
│   v15.1 │ a month ago │ MAPSRELEASES-6748 │ (@vmazaev) Sedem cli: sox support                                     │
├─────────┼─────────────┼───────────────────┼───────────────────────────────────────────────────────────────────────┤
│   v14.1 │ a month ago │ MAPSRELEASES-6747 │ (@robot-maps-sandbox) Update base image version: to 7744262           │
├─────────┼─────────────┼───────────────────┼───────────────────────────────────────────────────────────────────────┤
│   v13.1 │ a month ago │ MAPSRELEASES-6554 │ (@ivpeschinskiy) Remove missing in Figma icons script MAPSRENDER-2942 │
└─────────┴─────────────┴───────────────────┴───────────────────────────────────────────────────────────────────────┘
```

### release set-message

`sedem release set-message <path-to-service> <version> <message>`

Позволяет указать для релиза кастомное описание, которое будет отображаться в [release info](#release-info) и [release history](#release-history) вместо комментария к коммиту из Аркадии.

```bash
$ sedem release set-message maps/infra/teaspoon v18.1 "Add feature"
```

### release reject

`sedem release reject <path-to-service> <version> -m <reject-reason>`

Помечает релиз как "бракованный". При попытке выкатить такой релиз, седем будет выводить предупреждение.

```bash
$ sedem release reject maps/infra/teaspoon v17.2 -m "broken release"
Will reject v17.2: (@robot-maps-sandbox) Update base image version: to 7847239
Confirm? [y/N]: y
```

## Список изменений релиза (aka release changelog) { #changelog }

В ченджлог релиза попадают все коммиты [из истории запусков CI](services/sandbox#autobuild) между ревизией нового релиза и ревизией предыдущего релиза, а также между ревизией предыдущего релиза и ревизией релиза, выкаченного в стейбл.

{% note info %}

Если какое-то изменение не попало в ченджлог, нужно настроить [фильтры](https://docs.yandex-team.ru/ci/actions#filter) в конфиге CI (`a.yaml`).

Коммиты, для которых сборка была запущена вручную (по кнопке в CI), не попадают в ченджлог.

{% endnote %}

## Механизм двойного аппрува для sox-сервисов { #sox }

{% note alert %}

На текущий момент мы не можем гарантировать sox-сервисам прохождение аудита при использовании деплоев через sedem.
Это связано с тем, что сам sedem не является sox-сервисом, а значит у аудиторов могут возникнуть вопросы при смене схемы деплоя.
Настоятельно рекомендуется проконсультироваться с [нами](contacts.md), прежде чем планировать заезд sox-сервиса под sedem'а.

{% endnote %}

### Настройка

Для поддержки sox-сервисов в sedem добавлен механизм сбора двойных аппрувов на выкладку в `prestable` и `stable`.

Чтобы включить данный функционал, нужно указать в sedem-конфиге сервиса соответствующий флаг:
```yaml
# sedem_config/__all__.yaml

main:
    sox: true
```

Как только конфиг будет закоммичен, sedem включит соответствующий функционал для сервиса.

### Релизный цикл

Процесс релизов для sox-сервисов отличается следующим образом:
- при попытке выкатить сервис в `prestable` или `stable` создается согласование в [релизном тикете](#glossary), куда добавляются все участники abc-группы сервиса;
- необходимо собрать 2 подтверждения от участников согласования, чтобы иметь возможность выкатить сервис;
- как только 2 подтверждения будут собраны, необходимо **повторно выполнить команду** [release step](#release-step), чтобы запустить выкладку.

{% note info %}

Если автор деплоя состоит в abc-группе сервиса, то считается, что он автоматически согласовал выкладку, и достаточно собрать всего одно подтверждение, чтобы иметь возможность выкатить сервис.

{% endnote %}

```bash
$ sedem release step maps/infra/teaspoon v18.1 prestable
Loading service state............
Looking for release...
Found v18.1 (r7865833 / sbr #1997197085)
Will deploy v18.1 (r7865833) to "prestable": (@robot-maps-sandbox) Update base image version: to 7847239
Proceed to deploy? [y/N]: y
Starting deploy to prestable...
ERROR: Release v1.18 is awaiting approval for deploy to prestable in https://st.yandex-team.ru/MAPSRELEASES-7655
```

{% note warning %}

Если хотя бы один участник согласования отклонит выкладку (нажатием "Не ОК"), то данный релиз уже нельзя будет выкатить в выбранный стейдж.

Теоретически возможна ситуация, когда выкладка в престейбл была согласована, а в стейбл - нет.
В таком случае релиз все еще можно повторно выкатить в престейбл, и рекомендуется дополнительно воспользоваться командой [release reject](#release-reject), чтобы полностью исключить случайные выкладки данного релиза.

{% endnote %}

```bash
$ sedem release step maps/infra/teaspoon v15.1 stable
Loading service state............
Looking for release...
Found v15.1 (r7764441 / sbr #1942220968)
Will deploy v15.1 (r7764441) to "stable": (@vmazaev) Sedem cli: sox support
Proceed to deploy? [y/N]: y
Starting deploy to stable...
ERROR: Release v1.15 is declined to deploy to stable in https://st.yandex-team.ru/MAPSRELEASES-6748
```

### Информация о согласованиях в интерфейсе

Статус согласований отображается в выдаче команды [release history](#release-history):

```bash
$ sedem release history maps/infra/teaspoon -l 1
Loading service state..............
Release v15.1
SOX: [PRESTABLE APPROVED] [STABLE DECLINED]
Commit: https://a.yandex-team.ru/commit/7764441
Build task: https://sandbox.yandex-team.ru/task/874354750
St ticket: https://st.yandex-team.ru/MAPSRELEASES-6748
Released to: testing, prestable
Created at: 14:38 21 Jan 2021
Comment: (@vmazaev) Sedem cli: sox support
```

Кроме того, релизы, которые были отклонены при согласовании на выкатку в любой релизный стейдж, получают соответствующую пометку:

```bash
$ sedem release info maps/infra/teaspoon
Loading service state............
...
┌ Deploy (step) candidates (last 3) ───────────┬───────────────────────────────────────────────────────────────────────┐
│   Version │ Created      │ St ticket         │ Comment                                                               │
├───────────┼──────────────┼───────────────────┼───────────────────────────────────────────────────────────────────────┤
│ [D] v15.1 │ a month ago  │ MAPSRELEASES-6748 │ (@vmazaev) Sedem cli: sox support                                     │
├───────────┼──────────────┼───────────────────┼───────────────────────────────────────────────────────────────────────┤
│     v14.1 │ a month ago  │ MAPSRELEASES-6747 │ (@robot-maps-sandbox) Update base image version: to 7744262           │
├───────────┼──────────────┼───────────────────┼───────────────────────────────────────────────────────────────────────┤
│     v13.1 │ 2 months ago │ MAPSRELEASES-6554 │ (@ivpeschinskiy) Remove missing in Figma icons script MAPSRENDER-2942 │
└───────────┴──────────────┴───────────────────┴───────────────────────────────────────────────────────────────────────┘
...
```

## Автоматическое тестирование { #acceptance }

Sedem умеет ~~потыкать палочкой~~ протестировать ваш сервис после выкатки в определенный стейдж. Для этого седем запускает sandbox-задачи, указанные в конфиге сервиса, после завершения деплоя релиза.

Пример конфигурации:

```yaml
# sedem_config/__all__.yaml
acceptance:
  testing:
    - scheduler_id: '12345'
    - template_name: 'ANOTHER_ACCEPTANCE_TEST_RUNNING_BY_TEMPLATE'
```

{% note warning %}

Sedem никак не синхронизирует задачи между собой. Для этого предлагается настраивать семафоры из пользовательского кода.

{% endnote %}

При такой конфигурации после деплоя в `testing`-стейдж седем автоматически запустит (`manual run`) sandbox-шедулер `12345` и шаблон `ANOTHER_ACCEPTANCE_TEST_RUNNING_BY_TEMPLATE`.

Также седем передаст в параметр шаблона задачи:
+ `arcadia_url` — url для монтирования аркадии;
+ `sedem_service_name` — имя сервиса.

{% note warning %}

Все acceptance-тесты запускаются от робота [robot-task-master@](https://staff.yandex-team.ru/robot-task-master), поэтому для использования секретов в тестах у робота должны быть права на их чтение.

{% endnote %}

### Конфигурация стрельб в качестве acceptance-тестов

Для автоматического запуска нагрузочных тестов была написана sandbox-задача `MAPS_COMMON_LOAD_TESTING_TASK`. Она проводит нагрузочные тесты и проверяет sla.

[Инструкция по заведению нагрузочных тестов](services/nanny.md#load-testing)


## Проверка истории срабатывания мониторингов перед деплоем { #check-crits-before-deploy }

Sedem автоматически проверяет историю срабатывания мониторингов перед деплоем в следующий стейдж. Проверяются срабатывания мониторингов в предыдущем релизном стейдже с момента начала деплоя, т.е. при деплое релиза в prestable Sedem проверит историю срабатывания мониторингов с момента начала деплоя этого релиза в testing'е.

История срабатывания мониторингов проверяется независимо по всем деплой юнитам, входящим в релизный стейдж. Исключение составляют `unstable` и `load`/`stress` окружения няня-сервисов: все мониторинги в данных окружениях по умолчанию игнорируются.
```bash
$ ya tool sedem release step maps/infra/teapot v264.1 stable
Loading service state.........
Will deploy to stable v264.1 (r9232370): (@robot-maps-sandbox) Update base docker image to r9232313
WARNING: There were Juggler CRITs in "testing" stage since deploy (a day ago):
maps_core_teapot_testing: https://nda.ya.ru/t/PDKfv4Oa4rzCQd
(see https://docs.yandex-team.ru/sedem/services/nanny#check-crits-before-deploy for more info)
Proceed to deployment? [y/N]:
```

Sedem позволяет сконфигурить для каждого алерта, нужно ли его учитывать при проверке истории, для этого нужно выставить соотв. алертам флаг `ignore_on_deploy` с помощью [механизма фильтров](monitorings/alerts_metrics.md#filters):
```yaml
# filters.yaml
alerts:
  - filter:
      staging: testing
      service_name: my-flapping-alert
    body:
      ignore_on_deploy: true
```

Если хочется точечно проверять историю только некоторых алертов, то можно использовать следующую конструкцию фильтров:
```yaml
# filters.yaml
alerts:
  # Ignore all alerts CRITs on deploy
  - body:
      ignore_on_deploy: true

  # Check only alert1/alert2/alert3 CRITs on deploy
  - filter:
      service_name: alert1|alert2|alert3
    body:
      ignore_on_deploy: false
```

{% note warning %}

Изменения в списке проверяемых алертов не имеют обратной силы. Т.е. после того, как вы убрали алерт из списка, история его срабатываний ДО коммита конфига не обнуляется, и будет подсвечиваться sedem'ом.

{% endnote %}

При необходимости Sedem позволяет ограничить сверху размер временного окна проверяемой истории срабатывания алертов с помощью опции `max_alert_history_window` в [конфигурации релизного цикла](#deploy-config).
