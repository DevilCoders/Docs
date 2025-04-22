# `stand`

Команда для поднятия стенда. В неё заложена минимальная конфигурация стендов, вам необходимо указать только ветку и тег.

Практически полностью копирует поведение команды [`qtools release`](../README.md#release-environment), т.е. собирает и пушит образ (если его нет) и затем выкладывает окружение.

```sh
# npx qtools stand <branch> <tag> [OPTIONS] [-- DOCKER_BUILD_OPTIONS]
npx qtools stand dev xxxx
```

## Опции

* `--wait` (`-w`) — ждать ли окончания выкладки стенда, по умолчанию `false`.
* `--comment` — комментарий для Деплоя, по умолчанию по аналогии с командой `qtools deploy`.

## Приложение

По умолчанию стенды поднимаются в квоте геосервисов в приложении [maps-front-stands](https://deploy.yandex-team.ru/projects/maps-front-stands).

Для изменения вам необходимо указать поле `abcId` с ID сервисом, из которой будет использоваться квота. Также необходимо [расширить конфигурацию стейджа](#Расширение-стейджа).

## Балансер

По умолчанию балансировка стендов происходит через балансер [`front-stands.slb.maps.yandex.net`](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-stands.slb.maps.yandex.net/show/). Для изменения балансера используйте поле `deploy.stand.balancer.namespaceId`.

С переездом в AWACS появилась возможность поддерживать все домены одновременно. По умолчанию для формирования домена используется пакет [`@yandex-int/maps-stand-tools`](../../maps-stand-tools). Если вам необходимо указать свой хост, то используйте поле `.deploy.stand.balancer.host`.

При этом следующие строки будут заменены:
- `{{STAND_NAME}}` — идентификатор стенда.
- `.{{TLD}}` будет заменено на `(-team)?\.[\w.]+`.

Пример:

```js
{
    "deploy": {
        "stand": {
            "balancer": {
                "namespaceId": "your-namespace-id.slb.yandex.net",
                "host": "{{STAND_NAME}}.my.sub.domain.yandex.{{TLD}}"
            }
        }
    }
}
```

### Создание своего балансера

> TBD

## Репозиторий в Docker registry

По умолчанию используется префикс из `registry.prefix` и репозиторий `front-maps-stands-{{STAND_NAME}}`. Если вам нужен другой репозиторий, его можно указать в поле `deploy.stand.repository`:

```js
{
    // ...
    "deploy": {
        "stand": {
            "repository": "maps-foo-bar-stands"
        }
    }
}
```

## Название проекта

Проект — это единый идентификатор сервиса во фронтенде геосервисов: в идеале все ресурсы сервиса должны называться одинаково: ABC, приложение, репозиторий на гитхабе. В контексте стендов `project` используется для генерации названия стенда.

По умолчанию для стендов `project` генерируется из `abcServiceName` удалением из него префикса `maps-front-`: `maps-front-nmaps` -> `nmaps`. Если по какой-то причине (например, для монорепы) нужен нестандартный `project` для стендов, его можно задать параметром `deploy.stand.standNameProject`:

```js
{
    // ...
    "deploy": {
        "stand": {
            "standNameProject": "geoadv"
        }
    }
}
```

## Расширение стейджа

Если вы хотите добавить что-то специфичное для своего проекта, то используйте поле `deploy.stand.configPath`. В это поле необходимо передать путь до расширяемового файла в форме YAML.

```js
{
    // ...
    "deploy": {
        "stand": {
            "configPath": ".configs/deploy/stand.yml"
        }
    }
}
```

Сам файл по этому пути соответствует [спецификации Деплоя](https://wiki.yandex-team.ru/deploy/docs/dctl/#deploy-stage). Базовый конфиг для расширения можно посмотреть в этом репозитории: [`defaults/stand/stage.yml`](../defaults/stand/stage.yml).

### Примеры расширения конфигурации

**Изменение project_id**:

```yml
---
  meta:
    id: "your-project_{{STAND_NAME}}"
    project_id: your-project
```

**Изменение account_id**:

```yml
---
  meta:
    account_id: "abc:service:{{ID}}"
  spec:
    account_id: "abc:service:{{ID}}"
```

**Изменение размеров подов**:

```yml
---
  spec:
    deploy_units:
      app:
        multi_cluster_replica_set:
          replica_set:
            pod_template_spec:
              spec:
                disk_volume_requests:
                  - quota_policy:
                      # 10 Gb
                      capacity: 10737418240
                resource_requests:
                  # 1 Gb
                  memory_guarantee: 1073741824
                  memory_limit: 1073741824
                  # 0.125 CPU
                  vcpu_guarantee: 125
                  vcpu_limit: 125
```

**Изменение сети**:

```yml
---
  spec:
    deploy_units:
      app:
        network_defaults:
          network_id: "_YOUR_MACRO_"

```

**TVM и секреты**:

```yml
---
  spec:
    deploy_units:
      app:
        multi_cluster_replica_set:
          replica_set:
            pod_template_spec:
              spec:
                pod_agent_payload:
                  spec:
                    workloads:
                      - env:
                          - name: "YOUR_SECRET_VAR"
                            value:
                              secret_env:
                                alias: "{{SECRET_ID}}:{{VERSION_ID}}"
                                id: "YOUR_SECRET_VAR_IN_YAV"
                secrets:
                  "{{SECRET_ID}}:{{VERSION_ID}}":
                    secret_id: "{{SECRET_ID}}"
                    secret_version: "{{VERSION_ID}}"
        tvm_config:
          mode: "enabled"
          blackbox_environment: "Prod"
          client_port: 2
          clients:
            - secret_selector:
                alias: "{{SECRET_ID}}:{{VERSION_ID}}"
                id: "VAR_IN_YAV_WITH_TVM_SECRET"
              source:
                alias: "{{SOURCE_ALIAS}}"
                # TVM ID
                app_id: 1
              destinations:
                - alias: "{{DEST_ALIAS}}"
                  # TVM ID
                  app_id: 100500
```

## Раздельные шаги ```stand```

Если вам нужно разделить шаги выполнения команды `stand`, параметры можно передавать аргументами в функции `build`, `push`, `deploy` и `release`.

```sh
npx qtools build --branch=YOUR_BRANCH --tag=YOUR_TAG
```
