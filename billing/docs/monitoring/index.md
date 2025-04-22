# Мониторинг состояния сервисов
## Введение
В манифисенте есть команда, занимающаяся обновлением кластеров в Solomon и дашбордов при обновлении списка или содержания манифестов. Зона ответственности этой команды охватывает следующие сущности:

1. **Сервисные дашборды**. Создаются в двух местах: [Grafana](https://grafana.yandex-team.ru/dashboards/f/jgUN2QJnk/billing-dashboards) и [Monitoring](https://monitoring.yandex-team.ru/projects/newbilling-tarification/dashboards).
Описание дашбордов хранится в виде шаблона в одном YAML-файле, который считывается программой, и затем для каждого сервиса из директории с манифестами строятся запросы в Grafana и Monitoring.

2. **Дашборд с графом системы**. При обновлении списка манифестов на этом дашборде появляется новый сервис (или обновляются данные старого).
Хранится в [Grafana](https://grafana.yandex-team.ru/d/gsivUScnz/dashboard-tarifficator).

3. **Список кластеров в Solomon**. При  обновлении списка манифестов или изменении уже существующих список кластеров обновится соответствующим образом.
Хранится в [Monitoring](https://monitoring.yandex-team.ru/projects/newbilling-tarification/clusters/newbilling-tarification_faas-prod/host-groups/view).

## Хочу просто команду для обновления...

{% list tabs %}

- ... всего
    ```bash
    GRAFANA_OAUTH_TOKEN=<grafana token> MONITORING_UI_OAUTH_TOKEN=<solomon/monitoring token> /billing/hot/manificenta/manificenta dashboards-apply --config='billing/hot/manificenta/configs/prod/clients.yml' --template='billing/hot/manificenta/dashboard_templates/common.yml' --input='billing/hot/manificenta' --env='prod' --dc_names='vla,sas' --system_templates='billing/hot/manificenta/dashboard_templates/system_templates'
    ```

- ... только проектных дашбордов
    ```bash
    GRAFANA_OAUTH_TOKEN=<grafana token> MONITORING_UI_OAUTH_TOKEN=<solomon/monitoring token> /billing/hot/manificenta/manificenta dashboards-apply --config='billing/hot/manificenta/configs/test/clients.yml' --template='billing/hot/manificenta/dashboard_templates/common.yml' --input='billing/hot/manificenta'
    ```

- ... только кластеров Solomon
    ```bash
    MONITORING_UI_OAUTH_TOKEN=<solomon/monitoring token> /billing/hot/manificenta/manificenta dashboards-apply --config='billing/hot/manificenta/configs/test/clients.yml' --input='billing/hot/manificenta' --env='prod' --dc_names='vla,sas'
    ```

- ... только системных дашбордов
    ```bash
    GRAFANA_OAUTH_TOKEN=<grafana token> MONITORING_UI_OAUTH_TOKEN=<solomon/monitoring token> /billing/hot/manificenta/manificenta dashboards-apply --config='billing/hot/manificenta/configs/test/clients.yml' --input='billing/hot/manificenta' --system_templates=billing/hot/manificenta/dashboard_templates/system_templates
    ```

{% endlist %}

## Входные параметры
Список необходимых входных параметров зависит от того, какую из трёх задач выше требуется выполнить. Для всех них обязательным являются флаги

`--input`: **Директория с манифестами** содержит манифесты сервисов. Находится [здесь](https://a.yandex-team.ru/arc_vcs/billing/hot/manificenta/manifests).

`--config`: **Путь к файлу конфигурации**, описывающему список параметров, специфичных для каждого клиента, на котором создается дашборд (путь, директория, проект, etc.). Файлы конфигурации лежат [здесь](https://a.yandex-team.ru/arc_vcs/billing/hot/manificenta/configs).

Токены для клиентов передаются либо в файле конфигурации (ключ `oauth` в каждом из клиентов), либо через переменные окружения:

|        Grafana         |    Monitoring и Solomon     |
|:----------------------:|:---------------------------:|
| `GRAFANA_OAUTH_TOKEN`  | `MONITORING_UI_OAUTH_TOKEN` |

Токены можно получить, зарегистрировав приложение [вот тут](https://oauth.yandex-team.ru/client/new) и затем преобразовав полученный ID в токен [здесь](https://oauth.yandex-team.ru/) аналогично процессу, описанному [тут](https://yandex.ru/dev/oauth/doc/dg/tasks/get-oauth-token.html).

Далее в зависимости от команды список аргументов будет различным.
