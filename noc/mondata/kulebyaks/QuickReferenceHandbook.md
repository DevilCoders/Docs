* [Проверка статуса процесса](#проверка-статуса-процесса)
* [Хочу запустить свой скрипт](#хочу-запустить-свой-скрипт)
* [Хочу проверку на данных в solomon](#хочу-проверку-на-данных-в-solomon)
* [Настройка окружения](#настройка-окружения)

# Настройка окружения

Разворачиваем код:
```shell
git clone git@noc-gitlab.yandex-team.ru:nocdev/mondata.git
cd mondata
git checkout -b my_feature
```

Разворачиваем окружение:
```shell
python3 -m venv my_venv
my_venv/bin/python -m pip install -r requirements.txt
```

Создаем кулебяку и тестируем её([больше док](https://noc-gitlab.yandex-team.ru/nocdev/mondata/-/blob/master/kulebyaks/README.md#административная-секция)):
```shell
my_venv/bin/python update_kulebyaks.py --filter my_feature.yaml
```


# Проверка статуса процесса

```yaml
  templates:
    proc_status: { arguments:
                     { proc_name: slbcloghandler,
                       children_service: slbcloghandler_status,
                       service: slbcloghandler_proc_status },
                   override: { tags: [ noc_cold ] }
    }
```

**proc_name**: Имя процесса. Подставляется в pgrep -f "$proc_name".  
**children_service**: service сырых событий в juggler.  
**service**: service агрегата в juggler.  
```override: { tags: [ noc_cold ] }```: заменяет теги агрегата на указанные.
# Хочу запустить свой скрипт
Перед запуском новой проверки, необходимо предварительно договориться с деж. сменой, что она будет ее обрабатывать.
Для этого обязательно потребуется:
- инструкция как обрабатывать проверку
- help_key по которому будет идентифицироваться проверка
- приоритет проверки
- описание проверки по форме

Подробно передачи проверки в деж. смену можно посмотреть тут:
https://wiki.yandex-team.ru/noc/duty/monitoring-acceptance/

Делаем скрипт с таким выводом результата в формате juggler:
```python
import json
def main():
    try:
        res = check()
    except Exception as e:
        res = str(e)
    ret = {
        "events": [{
            "service": "my_script_service",
            "host": hostname,
            "description": res,
            "tags": ["rtapi_ping"],
            "status": res == "OK" and "OK" or "CRIT",
        }]
    }
    print(json.dumps(ret))
if __name__ == "__main__":
    main()
```
Здесь основная работа делается в check(). Он обмазан исключением, чтобы всегда был какой-то результат,
даже с исключением.  
В кулебяку добавляем запуск скрипта.
```yaml
  scripts:
    - { script: /path/to/my_proc.sh, arguments: [ olo ], interval: 90 }
```
И добавляем агрегат.
```yaml
  aggregates:
    - service: my_proc
      description: my script result
      tags: [ tags ]
      ttl: 300
      aggregator: more_than_limit_is_crit
      aggregator_kwargs: { percent: 1, nodata_mode: force_crit }
      children_service: my_script_service  # service из скрипта
```
# Хочу проверку на данных в solomon
Подробности про написание алерта в соломоне смотри в [доке](https://noc-gitlab.yandex-team.ru/nocdev/mondata/-/blob/master/kulebyaks/README.md#solomon).   

```yaml
  solomon:
    - alert_name: my super monitoring
      description: описание моего мониторинга
      program: |
        let flap = {project="myproject", service="network", sensor="flap", host="%(host)s"};
        let avg_flap = avg(flap);
        let message_val = to_fixed(flap, 0);
        alarm_if(flap > 9000);
      period: 900
      message_template: "сообщение в оповещение: флапы={{expression.message_val}}%"
      notification_channels: [ kulebyaks-noc-juggler ]
      help_key: myhelpkey
      juggler_tags: [ my_monitoring_tag ]
      juggler_service: my_monitoring
```

После создания алертов в соломоне, в жагглере появятся сырые события. 
Дальше нужно настроить агрегат, который сделает одно события из кучи сырых.  
Подробности про агрегаты смотри в [доке](https://noc-gitlab.yandex-team.ru/nocdev/mondata/-/blob/master/kulebyaks/README.md#juggler).
```yaml
  aggregates:
    - host: my_super_monitoring
      service: flap_status
      description: flap status
      tags: [ my_super_monitoring_tag ]
      ttl: 300
      aggregator: more_than_limit_is_crit
      aggregator_kwargs:
        percent: 5
        nodata_mode: force_crit
      children_service: my_monitoring
```
