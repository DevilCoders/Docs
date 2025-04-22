# Кастомизация service.toml

Использование любого из приведенных ниже способов кастомизации `service.toml`, будет означать:
* Сервис не сможет мигрировать из одной среды исполнения в другую: Deploy, Nanny, K8S.
* Сервис не сможет мигрировать из одного облака в другое: RTC, YC, AWS.
* Осложнится поддержка микросервиса, изменения могут привести к деградации.

## Overrides

Overrides - механизм, позволяющий указать специфичные для инфраструктурного сервиса параметры.

Механизмом можно переопределять настройки тех блоков в `service.toml`, которые имеют уникальный идентификатор `name`.

Например, мы хотим расширить описание нашего `workload` c `name="api"` в сервисе Y.Deploy

`service.toml`:

```toml
...

engine = "deploy"

[[box.workload]]
name = "api"

...
```

Для этого на одном уровне с файлом `service.toml` необходимо создать файл с произвольным именем, например `my-deploy-overrides.yaml` следующего содержания.

`deploy-overrides.yaml` _(примерная схема)_: 

```yaml
apiVersion: overrides.deploy/v1
kind: Override

spec:
    workloads:
      - id: env.stable.box.workload.api
        box_ref: box
        start:
            command_line: /bin/bash -c 'touch /tmp/healthy; sleep 30; rm -rf /tmp/healthy; sleep 600'
        liveness_check:
            container:
            command_line: cat /tmp/healthy
            time_limit:
                initial_delay_ms: 10000
                min_restart_period_ms: 5000
                max_restart_period_ms: 5000
```

## Unmanaged

Unmanaged - механизм, позволяющий полностью взять на себя управление одним или несколькими инфраструктурными сервисами.

Разберем список необходимых действий на примере с управлением балансировкой.

1. Из файла `service.toml` удаляем блоки `entrypoints` и `routes`.
2. Создаем директорию `infra` на одном уровне с `service.toml`.
3. Выполняем команду `ya infractl add` и выбираем `rtc`, `awacs`. У нас появиться файл полной спецификации AWACS созданный из шаблона по умолчанию.
4. Изменяем файл `awacs.yaml` под наши нужды, предварительно посмотрев необходимые параметры в других системах.