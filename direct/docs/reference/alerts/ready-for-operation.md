# ready_for_operation

[Примеры](https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Dready_for_operation%26(namespace%3Ddirect.prod|namespace%3Ddirect.test|namespace%3Ddirect.dev)) проверок.


## Описание { #description }
Проверятся готовность машины к работе. Основные правила записаны в `/etc/ready-for-operation/*.yaml`.

## Диагностика { #diagnostics }
Для проверки нужно зайти по ssh на ту машинку, про которую горит алерт.

1. Проверяем, что скрипт для ready-for-operation запускается.  
Запуск осуществляется через cron (`/etc/cron.d/yandex-du-ready-for-operation-common`):
   ```text
   */1 * * * * root timeout 50 /usr/local/bin/direct-spec /etc/ready-for-operation/*.yaml --juggler --service ready_for_operation >/dev/null 2>&1
   ```
   Смотрим логи запуска:
   ```sh
   grep 'direct-spec' /var/log/syslog
   ```
   Проверям, что процесс cron жив:
   ```sh
   ps aux | grep cro[n]
   ```
1. Проверяем, что машина не закрыта фаерволом и работает DNS.
   ```sh
   dig @localhost ya.ru
   nc -zv ya.ru 80
   ```
1. Cмотрим правила для iptables.
В ip6tables в секциях IPTBLOCKER-IN/IPTBLOCKER-OUT должно быть записей reject:
   ```sh
   ip6tables -L IPTBLOCKER-IN -nv | grep reject
   ip6tables -L IPTBLOCKER-OUT -nv | grep reject
   ```
   Нормальное состояние:
   ```text
   Chain IPTBLOCKER-IN (1 references)
    pkts bytes target     prot opt in     out     source               destination
   27193   92M RETURN     all      *      *       ::/0                 ::/0
   
   Chain IPTBLOCKER-OUT (1 references)
    pkts bytes target     prot opt in     out     source               destination
   28778  109M RETURN     all      *      *       ::/0                 ::/0
   ```
1. Проверяем работу juggler-client (смотрим логи и процессы)
   ```sh
   ps aux | grep juggler-clien[t]
   less /var/log/juggler-client/juggler-client.log
   ```
   Вариант перезапуска (KILL для надежности):
   ```sh
   pkill -9 -f cron
   pkill -9 -f juggler-client

   /etc/init.d/cron restart
   /etc/init.d/juggler-client restart
   ```
1. Идем в juggler и смотрим, что сырое событие отправляется: вкладка **Raw events** с фильтром по `service=ready_for_operation`,
[ссылка](https://juggler.yandex-team.ru/raw_events/?query=service%3Dready_for_operation).
