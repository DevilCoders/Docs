Автоматика для генерации агрегатов в juggler. Подробности работы жагглер читать тут
https://docs.yandex-team.ru/juggler/aggregates/basics.

Параметры агрегатов host, service, tags, description это параметры нового агрегата, а не фильтра по текущим событиям. Не перепутайте.

###### Отладка
Для внесения правок в juggler нужно иметь доступ к соответствующему namespace.

Нужен juggler-sdk:
```shell
pip3 install --index-url https://pypi.yandex-team.ru/simple juggler-sdk

```
Дамп определенного генератор:
```shell
./update_juggler.py --dump --filter hbf.yaml
```
Внесение правок в juggler:
```shell
./update_juggler.py --debug --filter hbf.yaml
```
###### Способы заведения агрегатов
### Точь-в-точь как в juggler api
```yaml
- host: grad  # параметры нового агрегата
  service: cpu  
  tags:
    - cpu_load
  description: grad cpu

  aggregator: more_than_limit_is_problem
  aggregator_kwargs:
    crit_limit: 50
    mode: percent
    warn_limit: 1
  
  children:
    - group_type: RT
      host: '{сервер grad}'
      service: cpu_util

  notifications:
    - description: grad cpu
      template_kwargs:
        login: gescheit
        method: telegram
        status:
          - CRIT
      template_name: on_status_change
  ttl: 120
```
### python-скрипт
```python
#!/usr/bin/env python3
# AUTHOR: noc@yandex-team.ru

from helpers import make_juggler_check, json_dump, TELEGRAF_TTL_INTERVAL, SERVICE_OOM_KILLER, get_conductor_hosts

def make_check():
    hosts = get_conductor_hosts("hbf_server", hostname=True)
    children = [{"host": host, "service": SERVICE_OOM_KILLER} for host in hosts]
    c = make_juggler_check(
        host="hbf_server", service="oom", tags=["oom"],
        aggregator="more_than_limit_is_problem",
        aggregator_kwargs={"mode": "percent", "crit_limit": 50, "warn_limit": 1},
        ttl=TELEGRAF_TTL_INTERVAL, description="kernel OOM killer",
        children=children,
        notifications=[
            {
                "template_name": "on_status_change",
                "template_kwargs": {
                    "status": ["CRIT"],
                    "login": "gescheit",
                    "method": "telegram"
                },
                "description": "oom"
            }
        ],
    )
    return [c]


if __name__ == '__main__':
    print(json_dump(make_check()))
```

### Шаблоны
```yaml
- host: hbf_sas
  checks:
    - telegraf_cpu: [101%, 90%]
  children:
    - group_type: CGROUP_SHORT
      host: nocdev-hbf-sas
```
Шаблон telegraf_cpu определен в папке juggler/templates/
Шаблоны работают так: берутся данные из агрегата, сливаются с шаблоном, а потом сливаются с аргументами шаблона.
В примере выше, telegraf_cpu это шаблон, [101%, 90%] это аргументы шаблона, а children... это данные агрегата.

В аргументах шаблона можно указать параметры разных типов.
1 - Список. Например "[101%, 90%]" и он заменит параметры warn_limit и crit_limit.
 Оба параметры должны быть с процентом, либо без. В juggler нельзя [смешивать](https://docs.yandex-team.ru/juggler/aggregates/aggregators#more_than_limit_is_problem "readme") проценты и абсолютные значения.
2 - Словарь. Сейчас поддерживается только один ключ times. Вида
```
{times: {work_time: ['0', '1'], weekend: ['1%', '101%'], night: ['2%', '101%']}}
```
для более тонкой настройки агрегата times.

### Макросы
Макросы это обычные функции на питоне(juggler/templates/*.py), 
которые возвращает готовый агрегат. В них возможно делать сложную логику.
Аргументы из агрегата в yaml передается как есть.

```yaml
- host: hbf
  checks:
    - slbcloghandler_macro: {hosts: [hbf.yandex.net]}
```
Вызовет ```slbcloghandler_macro(hosts=[hbf.yandex.net])```.