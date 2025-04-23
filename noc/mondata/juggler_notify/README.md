Автоматика для генерации подписок в juggler. Подробности работы жагглер читать тут
https://docs.yandex-team.ru/juggler/notifications/basics
Namespace поддерживаются ограниченно. Так как нет однозначного способа найти проверки созданные автоматикой, 
используется поиск по namespace и префиксу description.

Новый namespace добавляется в AVAILABLE_NAMESPACES в update_juggler.py. 
Права нужно дать пользователю robot-znoc. После чего автоматика будет синхронизировать оповещения в новом namespace.

Все события из zabbix(с тегом zabbix_noc) и solomon(noc_solomon) отправляются в juggler.
В события от zabbix в tags попадают теги из RT в транслите, теги указанные в mondata/discovery и автоматические теги по имени скрипта. Пример:
```
tag=zabbix_noc & (tag=server_videokonferentsiy | tag=discovery-xmpp_probe.py) & tag=Morozov_servernaya
```

###### Отладка
Для внесения правок в juggler нужно иметь доступ к соответствующему namespace.

Дамп определенного генератор:
```shell
update_juggler_notify.py --dump --filter hbf.yaml
```
Внесение правок в juggler:
```shell
update_juggler_notify.py --debug --filter hbf.yaml
```
###### Примеры подписки
```yaml
- description: grad solomon quota notify
  namespace: nocdev
  selector: host=grad_solomon_quota
  template_name: on_status_change
  match_raw_events: true
  template_kwargs:
      status:
          - {from: OK, to: CRIT}
          - {from: OK, to: WARN}
      login:
          - gescheit
      method:
          - telegram

```
- Python-скрипт
```python
#!/usr/bin/env python3
# AUTHOR: gescheit@yandex-team.ru

from helpers import make_juggler_notify, json_dump


def make_rules():
    rule = make_juggler_notify(
        selector="host=grad_solomon_quota & tag=solomon",
        template_name="on_status_change",
        template_kwargs={"method": ["telegram"], "login": "gescheit"},
        description="solomon quota",
        match_raw_events=True,
    )
    return [rule]
```
