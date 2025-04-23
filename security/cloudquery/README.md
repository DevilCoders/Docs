# Как начать пользоваться cloudquery

## Как поднять кластер PostgreSQL

1. Нужно пробросить [токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=8cdb2f6a0dca48398c6880312ee2f78d) и адрес API-ендпоинта в переменные среды:

```
export YC_ENDPOINT=gw.db.yandex-team.ru:443
export TF_VAR_oauth_token="AQAD-..."
```

2. Скорее всего, придется переопределить такие переменные в `vars.tf`, как:
    - `cloud_id` и `folder_id` (облако и каталог в yc.yandex-team.ru, можно посмотреть во вкладке Инфо)
    - `zone_id`
    - `pg_cluster_name`
    - возможно, параметры самого pg (например, `resource_preset_id`, `disk_size` или `backup_retain_period_days`)

Сделать это [можно](https://www.terraform.io/language/values/variables#variable-definitions-tfvars-files) либо в CLI (`terraform apply -var="cloud_id=foo"`), либо через file `.tfvars`, например `terraform apply --var-file=mdb-junk-cloud.tfvars`.

## Как написать конфигурацию для cloudquery

В cloudquery сбор информации из различных источников происходит с помощью провайдеров.
Почитать подробнее про каждый провайдер и его конфигурацию можно на [Cloudquery HUB](https://hub.cloudquery.io/).

Получившийся конфиг (например, `config.hcl`) нужно положить в каталог своего проекта `arcadia/security/cloudquery/<project>/`.

__Желательно__ в конфиге закрепить версию провайдера:
```hcl
cloudquery {
    provider "azure" {
        source = ""
        version = "v0.3.10"
    }
    // ...
}
```

## Как поднять свой cq-worker?

В Деплое запущен враппер ([cq-worker](https://bb.yandex-team.ru/projects/SEC/repos/cloudquery/browse)), который запускает cloudquery по расписанию.

Для того, чтобы поднять cq-worker со своей конфигурацией, нужно:

1. Создать каталог с проектом
2. Переименовать проект в pkg.json
3. Сделать актуальный `config.hcl`. Все переменные среды, необходимые провайдеру, лучше пробросить в `config.hcl`.
4. В каталоге `deploy` сделать `make all` (нужны права на запись в префикс `security/cq-packs/` Docker-registry. Или можно создать свой.)
5. При старте контейнера нужно скачать провайдеры. Сделать в deploy это можно через init command `cq-worker init --config cq-worker.yaml`
6. В настройках стейджа нужно использовать `nat64_local` для доступа в интернет под IPv4

