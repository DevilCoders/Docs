# Continuous Integration B2C-монорепозитория

## Технологии и полезные ссылки

Для CI проект B2C использует Arcadia New CI. Ранее CI жил на сочетании GitHub Hooks Api, Sandbox и ЦУМ.

Полезные ссылки, благодаря которым можно подробно узнать, как работает наш CI:
- CI в Arcadia ([docs.yandex-team.ru/ci](https://docs.yandex-team.ru/ci))
- Основы `a.yaml` ([docs.yandex-team.ru/ci/basics](https://docs.yandex-team.ru/ci/basics))
- Как устроены простейшие кубики на `common/misc/run_command` ([a.yandex-team.ru/arc/trunk/arcadia/ci/registry/common/misc](https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/common/misc))
- Документация b2c по переезду в Аркадию ([wiki.yandex-team.ru/users/nickshevr/marketfront-git-to-arc](https://wiki.yandex-team.ru/users/nickshevr/marketfront-git-to-arc))

## a.yaml: от галочки в Аркануме до кода кубика

Все CI проверки описываются декларативно в файле [a.yaml](https://a.yandex-team.ru/arc_vcs/market/front/apps/marketfront/a.yaml).

### CI в интерфейсе

В интерфейсе Аркануме CI может выглядеть как проверки на пулл-ревквест или пайплайн на мерж в транк.

![CI-проверки на пулл-реквест в интерфейсе Арканума](_assets/ci-checks-on-pr.png)

{% note tip %}

Некоторые пайплайны, например, релизный, все еще располагаются в ЦУМе. Это ни хорошо, ни плохо. Возможно в будущем они окажутся в New CI.

{% endnote %}

![Кубики в интерфейсе Арканума](_assets/ci-jobs.png)

Кубики, связи между ними и ссылки на них генерируются непосредственно через `a.yaml`.

### Флоу и экшены

Пайплайн — это флоу. На события (экшены) можно вызывать запуск пайплайна. Подробнее описано в официальной документации CI (https://docs.yandex-team.ru/ci/actions).

В нашем `a.yaml` это выглядит примерно вот так:

```yaml
ci:
  actions:
    pr-white-desktop:
      title: white-desktop pr checks
      flow: white-desktop-pr-flow
      flow-vars:
        flow-tag: 'white-desktop'
      triggers:
        - on: pr
          into: trunk
          filters:
            - sub-paths: [ '**' ]
              not-sub-paths:
                - api/**
                - business/**
                - pokupki/**
                - market/platform.touch/**

  flows:
    white-desktop-pr-flow:
      title: PR white-desktop flow
      jobs:
        check-flowtype: *check-flowtype-job
        check-jest: *check-jest-job
        check-eslint: *check-eslint-job
```

{% note tip %}

Переезжая в Аркадию мы приняли решение условно разделить наш проект на CI-зоны (`flow-tag`): `src`, `white-src`, `white-desktop`, `fapi` и т.д.

{% endnote %}

Каждый `flow-tags` — это отдельный `flow` и отдельный `flow-vars`. Так можно построить отдельные проверки как для `src` (core-части всех приложений), так и для узких частей, как `white-fapi`.

### Кубики

Джобы (или по-простому "кубики") могут быть определены как простейшие bash-скрипты через `run_command` или как сложные Sandbox таски.

{% note warning %}

Аркадия New CI позволяет писать ифы, и определять из джоб те флоу, в которых они могут быть вызваны. Это неправильно!

Мы стремимся описывать код максимально декларативно, активно переиспользуя кубики и управляя их подключением из флоу.

{% endnote %}

Пример кубика:

```yaml
shared:
  jobs:
    check-flowtype: &check-flowtype-job
      title: Flow Typechecking
      task: common/misc/run_command
      requirements:
        cores: 1
        sandbox:
          client_tags: MULTISLOT | GENERIC
          container_resource: 2864846541
          dns: dns64
          priority:
            class: SERVICE
            subclass: NORMAL
          semaphores:
            acquires:
              - name: market_front_ci_semaphore
      input:
        config:
          arc_mount_config:
            enabled: true
          logs_config:
            redirect_stderr_to_stdout: true
            stdout_ci_badge: true
          secret_environment_variables:
            - key: AWS_ACCESS_KEY_ID
              secret_spec:
                key: 'robot-metatron-s3-keyid'
            - key: AWS_SECRET_ACCESS_KEY
              secret_spec:
                key: 'robot-metatron-s3-secretkey'
            - key: ST_OAUTH_TOKEN
              secret_spec:
                key: 'robot-metatron-st-token'
          cmd_line: |
            export PATH=$PATH:/opt/nodejs/16/bin

            cd ${context.config_info.dir}
            npm run arc-ci:${flow-vars.flow-tag}:flow
            mkdir -p $RESULT_RESOURCES_PATH/txt_reports

            mv txt_reports/* $RESULT_RESOURCES_PATH/txt_reports
          result_resources:
            - path: txt_reports
              description: Flow result
              type: OTHER_RESOURCE
              compression_type: none
              optional: false
              ci_badge: true
              ci_badge_path: report.txt
```

Код наших кубиков запускается в общем маркетовом контейнере. Его настройки мы скрываем за ссылкой на `&requirements`. Общие настройки кубика также переиспользуем через (`&common-run-command-config`).

`export PATH=$PATH:/opt/nodejs/16/bin` позволяет начать вызывать `node` и `npm` в коде джобы.

{% note info %}

В CI состоянии Аркадии: один мерж коммит. Состояние `arc reset --hard HEAD^` переводит в состояние "до изменений". При этом количество коммитов в ветке неважно, в CI всегда все как один коммит поверх ревизии без изменений.

{% endnote %}

{% note warning %}

Мы не любим Python. А еще меньше мы любим Bash. Поэтому код джоб старается выполнить как можно меньше команд, а основная часть проверки, как правило, выносится в npm-скрипт.

```json
{
  "scripts": {
    "arc-ci:white-src:flow": "cd market && npm run bootstrap && npm run ci:flow && cp -r txt_reports .."
  }
}
```

{% endnote %}

{% note alert %}

Для описания npm-скриптов нужно использовать только корневой `package.json`. Белый FAPI, например, не содержит файла `package.json` совсем. Множественные `package.json` — это наследие слияния репозиториев, не нужно на них завязываться.

{% endnote %}

Например, ответственность в решении задачи по запуску проверки Флоу решается так:
- Кубик и содержимое `cmd_line`:
    - Настройки Sandbox
    - Доступы
    - Настройки окружения
    - Путь до отчета
- npm-скрипт (`arc-ci:...`)
    - Запуск кода джобы на удобном языке
    - Перемещение отчета в корень репозитория
- Код проверки
    - Продуктовый код
    - Запись в stdout/файл с отчетом

Так случилось, что раньше ci-проверки описывались в проектных/платформенных папках. Теперь описываются в корневом `package.json`. Целью "перенести папочку txt_reports" теперь управляет корневой скрипт `arc-ci:...`.

### Связи между кубиками

Для облегчения нагрузки на нашу общую квоту в Sandbox монжо запускать некоторые проверки по условию. Так проверка на сборку будет запущена только в том случае, если проверены типы и код-стайл.

```yaml
jobs:
  check-build: &check-build-job
    title: Build Test
    needs:
      - check-eslint
      - check-flowtype
```

![Кубик сборки ожидает кодстайл](_assets/ci-dependencies.png)

{% note warning %}

Это не панацея. Множественные зависимости могут замедлить TTM.

{% endnote %}

## Правила и полезные практики

Создавая `a.yaml` и выработали общие практики и правила. Утверждается, что они помогут нам всем сохранить удобство в управлении CI.

### Джобы не должны зависеть от Флоу

`jobs` не должны быть зависимы от конкретного `flow`. Параметр `needs` не нужно указывать при объявлении джобы, напротив, он должен быть при объявлении джобы внутри Flow.

```yaml
shared:
  jobs:
    check-typescript: &check-typescript-job
      # Содержимое проверки
    check-build: &check-build-job
      # Содержимое проверки
ci:
  flows:
    my-flow:
      title: My Flow
      jobs:
        check-typescript: *check-typescript-job
        check-build:
          <<: *check-build-job
          needs: check-typescript
```

Удобная возможность синтаксиса a.yaml — flow-vars. С ее помощью можно строить джобы независимо от окружения.

```yaml
shared:
  flow-vars:
    flow-var-desktop: &flow-var-desktop
      name: desktop
    flow-var-touch: &flow-var-touch
      name: touch

ci:
  actions:
    pr-desktop:
      flow-vars: *flow-var-desktop
      flow: my-flow
    pr-touch:
      flow-vars: *flow-var-touch
      flow: my-flow
  flows:
    my-flow:
      title: My Flow
      jobs:
        check-build:
          title: Check Build in Platform ${flow-vars.name} # Обращение к переменной
```

{% note info %}

Чтобы джобы были абстрактными, лучше не писать код самих проверок внутри них. Например, в B2C код проверки флоу для разных платформ отличается кардинально, поэтому понадобился дополнительный слой с маппингом проверок.

{% endnote %}

### Ссылки, JMESPath и объект `context` — хорошие инструменты

Если код дублируется, нужно использовать ссылки (`*`, `&`). Это может быть полезно не только для объектов, но и для текстовых вставок.

Внутри `a.yaml` [работают выражения JMESPATH](https://docs.yandex-team.ru/ci/expression#syntax). А из кода проверок можно вызывать объект [контекста для получения параметров среды](https://docs.yandex-team.ru/ci/flow#context).

В синтаксисе Yaml есть такие же спреды, как и в JS (`<<`). Работает с объектами, но не с массивами.

```yaml
shared:
  common-vars:
    # Имя текущей ветки
    branch-name: &var-branch-name ${not_null(context.launch_pull_request_info.vcs_info.feature_branch, 'trunk')}

    # Имя текущей ветки для деплоя в CMS (@launch ПРИ ЗАПУСКЕ ЗАМЕНИТЬ НА `trunk`)
    cms-head-branch: &var-cms-head-branch ${not_null(context.launch_pull_request_info.pull_request.id, 'users/nickshevr/test-trunk')}

    # Тикет для старта мультитестинга
    ticket-id: &var-mt-ticket-id ${not_null(context.launch_pull_request_info.issues[0].id, 'marketfront-17830')}

    # Путь в Аркадии до корня проекта
    arc-path: &var-arc-path /market/front/apps/marketfront

    # Устойчивый ключ для кэширования ресурсов внутри одного флоу
    resource-version: &var-resource-version pr-${not_null(context.launch_pull_request_info.pull_request.id, 'trunk')}

    # Является ли текущая ветка транком
    is-trunk: &var-is-trunk ${to_string(context.branch == 'trunk')}

    # Строковый литерал `true` (парсер конфига не работает со логическими типами, только со строками и объектами)
    true: &var-true 'true'

    # Строковый литерал `false` (парсер конфига не работает со логическими типами, только со строками и объектами)
    false: &var-false 'false'
```

### Использовать нужно тот инструмент, который лучше подходит

Код Sandbox-тасок обычно использует Python. При написании новых тасок стоит ответить на вопросы:
- Можно ли решить задачу без новой таски
- Как эту таску можно будет развивать и поддерживать (как будут устроены тесты, например)

Уже сейчас можно избежать нового Python-кода, и использовать внутри кубиков Bash или JavaScript. Это более привычные инструменты для B2C-разработки.

### Тернарник JMESPath

```js
condition && true || false
```

### Получить все ресурсы с предыдущего шага

Иногда может быть полезно получить все артефакты из предыдущих задач. При этом их количество может быть неизвестно. Для этого можно воспользоваться финтом:

```yaml
my-job:
  title: My Job
  task: common/misc/run_command
  input:
    config:
    fixed_sandbox_resources: >-
        ${tasks.*.resources[]|[?type == 'OTHER_RESOURCE' && attributes.type == 'lighthouse_metrics'].{resource_id: id, key: attributes.id}}
    cmd_line: |
        my-script {${tasks.*.resources[]|[?type == 'OTHER_RESOURCE' && attributes.type == 'lighthouse_metrics'].attributes.id | join(reverse('{ }'), @)}}
```

Выражение `{tasks.*.resources}` получает все задачи на предыдущем шаге, `|[]` -- фильтр, а `.{}` -- маппинг.

В описании скрипта можно обратиться к этим ресурсам точно также, получив их имена. Далее нужно каждое имя обернуть в `{ }`, чтобы выстроилась строка `{name1} {name2} ...`.

```python
condition && true || false
```

## Антидроп

Одна из классических задач в CI: сравнить состояние до изменений и после. В старой версии CI за это отвечала Sandbox-таска `MARKET_FRONT_CI_ANTIDROP`. Теперь эту задачу можно решить гораздо легче на JS.

### Обязательность проверки

В B2C очень давно существует проверка Flow Coverage. И она необязательна. От задачи к задаче ее показатели этой проверки могут падать или расти хаотично. Нужна ли эта проверка вообще — вопрос спорный. Но она точно не должна быть на критическом пути, и не должна потреблять основные ресурсы CI.

Для решения задачи "сделать проверку недеградации обязательной", все antidrop-проверки разделены на обязательные и экспериментальные.

### Как завести свою антидроп-проверку

1. Прилинковать новую antidrop-проверку к флоу-тэгу:

```yaml
shared:
  settings:
    flow-vars:
      flow-vars-white-src:
        antidrop-config:
          required:
            - id: my-custom-check
              title: My Custom Check Title
              required: true # Кубик должен упасть, если проверка показала отрицательный результат
              strategy: my-strategy # Одна из доступных стратегий
```

2. Прописать в корневом `package.json` запуск сбора состояния:

```json
{
  "scripts": {
    "arc-ci:white-src:antidrop:my-custom-check": "node ./scripts/ci/my-coverage.js > value.txt"
  }
}
```

{% note warning %}

Результат на этом шаге нужно обязательно сохранить в корневом файле `value.txt`.

{% endnote %}

3. Описать стратегию сравнения или выбрать любую из существующих:

Стратегии по сравнению описываются в JS-скрипте ([a.yandex-team.ru/arc_vcs/market/front/apps/marketfront/scripts/ci/antidrop/core.js](https://a.yandex-team.ru/arc_vcs/market/front/apps/marketfront/scripts/ci/antidrop/core.js)).

В результате в нужном пайплайне должна появиться новая antidrop-проверка.

![Кубик сборки ожидает кодстайл](_assets/ci-antidrop-jobs.png)

## Мерж в транк

Существует два подхода к тому, как жить в монорепозитории. Рассмотрим оба из них.
- **Trunk based**. При таком подходе коммиты после прохождения код-ревью сразу мержатся в транк. Релизная машина стартует со свежей версией транка.
- **С релизной веткой**. В этом случае мерж в транк напрямую запрещен. Релизная команда набирает коммиты, создает релизную ветку, а после прохождения релиза коммиты оказываются в транке.

В то время как большинство команд в Аркадии живут по принципу trunk-based, мы не можем на него перейти прямо сейчас. Преимущество такого подхода для CI заключается в том, что состояние "эталона" протухает относительно долго, и сложные артефакты можно, например, кэшировать.

Одним из инструментов по работе с состоянием транка является **пайплайн по мержу в транк**.

### Цели

На каждый мерж в транк стартует несколько пайплайнов. Основные цели:
- обновить второстепенную статику (документации, статистики);
- обновить CMS-схему;
- закэшировать сложные ресурсы (такие как артефакты Статоскопа).

### Конфиг пайплайна

Как и другие флоу CI, пайплайн по мержу в транк описывается в `a.yaml` конфиге.

```yaml
ci:
  releases:
    testing-white-desktop:
      title: white-desktop merge trunk jobs
      flow: white-desktop-trunk-flow
      flow-vars: *flow-vars-white-desktop
      auto: true
      filters:
        - sub-paths: [ '**' ]
          not-sub-paths: *not-sub-paths-white-desktop

  flows:
    white-desktop-trunk-flow:
      title: Trunk white-desktop flow
      jobs:
        build-statoscope-stats: *build-statoscope-stats-job
        deploy-statface: *deploy-statface-job
        deploy-statics: *deploy-statics-job
```

{% note tip %}

Мы выбрали релизы (`releases`), а не экшены (`actions`), чтобы можно было добавить мониторинги и следить за состоянием этих пайплайнов.

{% endnote %}

### Деплой статики

В прошлом мире для публикации документаций или небольших текстовых отчетов использовался Github Pages. Теперь в качестве хранилища используется S3, и утилита `ya tool aws` в качестве клиента.

Конфигурация загрузки на S3 скрыта за кубиком `deploy-statics`. Использовать загрузку можно так:

```yaml
flow-vars:
  flow-vars-src:
    flow-tag: 'src'
    statics-artefacts:
        # id, который будет использоваться на хук в package.json
      - id: entities
        # Заголовок кубика
        title: Entities Codehealth
        # Путь от корня marketfront до артефакта
        artefact_path: reports
        # Путь опубликованного артефакта на s3
        s3_path: entities-codehealth
```

```json
{
    "scripts": {
        "arc-ci:white-src:pre-deploy-statics:entities": "npm run bootstrap && npm run report:codehealth"
    }
}
```

В результате в контейнере будут выполнены действия:
- Запустится npm-скрипт с пре-деплой хуком
- Результат будет загружен на s3

{% note info %}

Если пре-деплой хук должен быть заполнен, даже если не используется.

{% endnote %}
