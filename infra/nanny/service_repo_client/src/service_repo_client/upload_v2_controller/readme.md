## Общее

Инструмент работает с описанием сервиса в директории запуска. Для работы необходима другая директория для хранения файлов внутреннего представления nanny. Она указывается с помощью параметра ``-d``
или ``--dir``.

## Get

Скачивает состояние сервиса nanny и создаёт файлы с текущей конфигурацией в директории запуска.

Пример для [сервиса](https://dev-nanny.yandex-team.ru/ui/#/services/catalog/service_repo_test/) ``service_repo_test`` в dev инсталяции nanny

    scli -T -d ~/tmp/service_repo_client_data get_v2 service_repo_test

## Upload

Скачивает состояние сервиса nanny, сравнивает его текущее состоние с локальной версией. После подтверждения обновляет состояние в nanny

Пример для [сервиса](https://dev-nanny.yandex-team.ru/ui/#/services/catalog/service_repo_test/) ``service_repo_test`` в dev инсталяции nanny

    scli -T -d ~/tmp/service_repo_client_data upload_v2 service_repo_test

### Управление атрибутами секции Information

#### Обязательные параметры

    id: service_repo_test  # id сервиса в nanny
    abc: 2776  # id родительского сервиса в abc
    category: /users/zhshishkin/  # расположение сервиса в иерархии сервисов nanny
    description: Best service  # Описание

#### Опциональные параметры

    queue: TEST  # очередь для тикетов nanny

#### Рецепты Alemate

    recipes:
      activate:  # рецепты для активации инстансов
        default:  # id рецепта в сервисе
          context:  # контекст шаблониазации
            key: value
            other_key: some_value
          description: Activate  # человесеское описание
          name: _activate_only_service_configuration.yaml  # id шаблона
      prepare:  # рецепты для создания инстансов
        default:
          context: { }
          description: Prepare
          name: _prepare_service_configuration.yaml

#### Интеграция с sandbox

    sandbox_release_rules:
      - description: 'Update geobase in service'
        expression: sandbox_release.release_type in ("stable", "prestable",)  # выражение для матчинга
        task_type: GEODATA6BIN_STABLE_BUILDER  # тип релизной задачи
        resource_type: GEODATA6BIN_STABLE  # тип ресурса

        ticket_priority: NORMAL  # приоритет создаваемого nanny-тикета
        queue_id: TEST  # очередь для тикетов (optional)
        responsible_persons:  # ответсвенные за тикет (optional)
          - zhshishkin
        scheduling:  # включение автоматического коммита (optional)
          priority: NORMAL  # приоритет нового снепшота
          activate_recipe: default  # id рецепта для активации (optional)
          prepare_recipe: default  # id рецепта для создания инстансов (optional)
        approve_policy:  # политика подтвердения (optional)
          type: MULTIPLE_APPROVE  # пока только MULTIPLE_APPROVE
          approves_count: 2  # число подтверждений
          approvers:  # подтверждающие
            logins:
              - zhshishkin
            groups:
              - "123"
            mandatory_approvers:  # обязательные подтверждающие (optional)
              - zhshishkin

#### Автоматизированная выкладка

    scheduling_policy:
      type: BASED_ON_SNAPSHOT_PRIORITY  # тип автоматизации
      activate_recipe: default  # id рецепта для активации
      prepare_recipe: default  # id рецепта для создания инстансов

#### Мониторинг

###### Деплой

    monitoring:
      deploy:
        timeout: 3600  # число секунд активации, спустя которое загорится алерт
        logins:  # логины получателей. Могут быть id чатов
          - zhshishkin
        methods:  # каналы доставки juggler
          - telegram

#### Интеграция с infra

    infra_notifications:
      service_id: "2892"
      environment_id: "4525"

### Управление атрибутами секции Runtime

Они все находятся во вложенном объекте с ключом ``runtime_attrs``

    runtime_attrs:
      ...

#### Файлы / ресурсы

###### Статические файлы

    resources:
      static_files:
        fakefile:  # имя файла в контейнере
          content: fakefile  # имя локального файла в папке static_files
          is_dynamic: false  # является ли файл динамическим

###### Sandbox ресурсы

    resources:
      sandbox_resources:
        push_client:  # имя файла в контейнере
          resource_id: '566094677'  # id ресурса в sandbox
          is_dynamic: false  # является ли файл динамическим
          disable_updates: true  # (optional) см далее

``disable_updates: true`` отключает принудительно изменение параметров файла, если он уже есть в сервисе. То есть если файл с таким именем в секции sandbox ресурсов уже есть, то он не будет изменен.
Если нет, то он будет добавлен. Этот параметр полезен, когда надо добавить ресурс, который обновляется средствами интеграции с sandbox

#### Дополнительные папки (Volumes)

###### Шаблонизированная

    volumes:
      template:
        configs:  # имя папки
        - src: template_async_api_config.yaml  # файл для шаблонизации
          dst: async_api_config.yaml  # итоговый для шаблонизации, будет в папке

###### С секретами из Ya Vault

    volumes:
      vault_secret:
        yndx.uslugi.money.certs:  # имя папки
          secret_uuid: sec-01eb17nf0ba4kb752qs14rg23d  # uuid секрета
          version_uuid: ver-01ec27qge4pk8qk4p0frnkjvmd  # uuid версии секрета

###### ITS

    volumes:
      its:
        controls:  # имя папки
          url: http://dev-its.yandex-team.ru/v1  # (optional) по умолчанию http://its.yandex-team.ru/v1
          polling_period_in_second: 60  # (optional) по умолчанию http://its.yandex-team.ru/v1
          max_retry_polling_period_in_second: 300  # (optional) по умолчанию http://its.yandex-team.ru/v1

В самом простом варианте можно написать так

    volumes:
      its:
        controls: { } # имя папки

###### С секретами из Nanny Vault (deprecated)

    volumes:
      nanny_secret:
        yndx.uslugi.money.certs:  # имя папки
          keychain_id: "..."  # поля заполнятся инструментом сами
          secret_id: "..."  # изменять их не надо
          revision_id: "..."  # для новых секретов надо использовать ya vault

#### Дополнительная инициализация

    containers:
      init:
        create_dirs: |  # название инициализации
          # shell script, выполняется через /bin/sh -c command
          mkdir -p /logs/push_client_state && mkdir -p {BSCONFIG_IDIR}/logs

#### Основные контейнеры работы сервиса

    containers:
      runtime:
        logrotate:  # название контейнера
          command: |  # команда запуска, не shell script
            /bin/bash -c |
            "while true; do sleep 600 && logrotate -s /logs/logrotate.state logrotate.conf; done"

    Далее идут необязательные поля, расположенные на одном уровне с сommand

##### Переменные окружения

###### Константные

    environment_variables:
      PRODUCT_ORDER_SECONDS_TO_RENEW: '300'

###### Из Ya Vault

    environment_variables:
      VAULT_SECRET:
        secret_uuid: sec-01eb17nf0ba4kb752qs14rg23d  # uuid секрета
        version_uuid: ver-01ec27qge4pk8qk4p0frnkjvmd  # uuid версии секрета
        field: secret  # (optional) требуется для выбора конкретного ключа из секрета

###### Из Nanny Vault (deprecated)
Не рекомендуется к использованию.
Вместо изменения лучше перейти на Ya Vault

    environment_variables:
      CSRF_TOKEN_SECRET:
        keychain_id: ydo_backend_secrets
        revision_id: dd073f2f-a1e2-4001-9b77-0d84dcfaf638&initial-revision&1535472000503
        secret_id: csrf_token

##### Правила рестарта

    restart_policy:
      min_period_seconds: 1  # (optional)
      max_period_seconds: 60  # (optional)
      backoff: 2  # (optional)
      jitter_seconds: 20  # (optional)

##### Проверка готовности сервиса

    readiness_probe:
      period_seconds: 5  # (optional) по умолчанию 5
      backoff: 2  # (optional) по умолчанию 2
      min_period_seconds: 5  # (optional) по умолчанию 5
      max_period_seconds: 60  # (optional) по умолчанию 60
      handlers:
        - command: nc -vz localhost {BSCONFIG_IPORT}

Есть несколько доступных проверок, которые можно совмещать

###### Shell script

    handlers:
      - command: nc -vz localhost {BSCONFIG_IPORT}

###### TCP port check

    handlers:
      - port: '80'

###### Http check

    handlers:
      - path: /ping  #  запрос
        port: ''  # (optional) по умолчанию означает {BSCONFIG_IPORT}

##### Хендлер остановки сервиса

    pre_stop_handler:
      graceful_period_seconds: 60  # (optional)
      termination_period_seconds: 60  # (optional)
      all_handlers_barrier: 'IGNORE'  # (optional)
      handler:
        command: curl -o /dev/null -6s "http://localhost:{BSCONFIG_IPORT}/admin?action=shutdown"
          && exit 0 || exit 10

Можно использовать любой другой хендлен, описанный в предыдущем пункте

##### Хендлер переоткрытия файла логов

    reopen_log_handler:
      command: curl -o /dev/null -6s "http://localhost:{BSCONFIG_IPORT}/admin?action=shutdown"
        && exit 0 || exit 10

Можно использовать любой другой хендлен, описанный в предыдущем пункте

##### Unistat ручка

    unistat:
      - path: _golovan_with_zeros  # запрос
        port: '{BSCONFIG_IPORT}'  # (optional) по умолчанию {BSCONFIG_IPORT}


### Управление атрибутами секции Auth

    auth_attrs:
      owners:  # владельцы сервиса, могут всё
        logins:  # список логинов
          - zhshishkin
        groups:  # список групп, поддерживает abc, staff
          - svc_ydo_devops
          - yandex_search_tech_spam_3302_2902
      configuration_managers:  # могут редактировать атрибуты сервиса
        ...
      operation_managers:  # могут начинать и останавливать выкатку
        ...
      observers:  # добавляются в связанные тикеты
        ...
