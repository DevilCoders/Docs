
## Соломон
### Добавление алерта в [Соломон](https://solomon.yandex-team.ru)
В папке solomon лежат скрипты, в котором написано на каких хостах и что нужно проверять. Пример скрипта:
```python
#!/usr/bin/env python3
# AUTHOR: user@yandex-team.ru
import json

from helpers import get_rt_hosts, make_solomon_alerts


PROGRAM_TMPL = r'''
let rx = {
    project='noc',
    cluster='shard*',
    sensor='rx_packets',
    service='network',
    host='%(host)s',
    ifname=~'(?i)(^cxl|^Lagg|^mce|^ix)[^\.]*$'
};

let rx_sum = sum(sum(rx) by host);
'''


def make_alerts():
    hosts = get_rt_hosts('({NAT64 gateway} or {decapsulator} or {TUN64 gateway}) and not {в оффлайне}')
    return make_solomon_alerts(
        hosts=hosts,
        alert_name='tx_rx_diff',
        program_tmpl=PROGRAM_TMPL,
        check_expression='rx_sum > 500',
        period_millis=900000,
        delay_seconds=2400,
        notification_channels=["noc-juggler"],
        annotations={
            'tx_avg': '{{expression.tx_avg}}',
            'rx_avg': '{{expression.rx_avg}}',
            'diff': '{{expression.diff}}',
        }
    )


if __name__ == '__main__':
    print(json.dumps(make_alerts(), indent=2))
```
Или в формате yaml
```yaml
# AUTHOR: noc@yandex-team.ru

- alert_name: io_load
  # io_time: this value counts the number of milliseconds during which the device has had I/O requests queued.
  program: >
    let top1 = top(1, "avg", (non_negative_derivative({cluster="all", service="diskio", sensor="io_time", host="plumbum"}))/10);

    let avg_last = avg(top1);

    alarm_if(avg_last > 95);
  rt: "[работает telegraf] and {$cn_sas1-grad2}"
  period: 900
  notification_channels: []
  annotations: []
  help_key: "diskio"
  message_template: "diskio"
```

Подробнее про возможности алертов см. в [документации Соломона](https://wiki.yandex-team.ru/solomon/userguide/alerting/). Обратите внимание, что `program_tmpl` должен содержать плейсходер `%(host)s`, туда подставится хост для каждого алерта.

В поле `notification_channels` задаются способы алертинга. Управлять ими можно в [интерфейсе Соломона](https://solomon.yandex-team.ru/admin/projects/noc/channels/).

### Отладка проверок solomon'а
Обновить алерты по фильтру(затрутся автоматикой):
```bash
./update_solomon.py --filter filename.py --debug
```
Есть опция --dump - только вывод результата генерации алертов.
