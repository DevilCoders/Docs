# Хосты, свитчи, сеть, etc...
## Сеть
### Посмотреть логи начального конфигурирования сети {#net-logs}
**Внимание для следующих действий у вас должен быть доступ к dom0 машине и права пользователя root**
Посмотреть логи начального конфигурирования сети
`cat /var/log/upstart | grep network`
`journalctl -u ifup@eth0.service`
Посмотреть лог конфигурирования VLAN на машине
`cat /var/log/yandex-netconfig-fixall | grep "Push" or "VLAN"`

### Периодически не устанавливаются TCP соединения {#connection-timeouts}
В случае проблем с сетью пользователь может видеть проблемы с таймаутом установки TCP соединений:

```
$ curl -v https://blackbox.yandex-team.ru/
* About to connect() to blackbox.yandex-team.ru port 443 (#0)
*   Trying 2a02:6b8:0:3400::29... Connection timed out
*   Trying 213.180.205.29... Failed to connect to 213.180.205.29: Network is unreachable
```

Важно попробовать сделать reproduce, например, запустив curl в цикле на длительное время, например:
`while :; do date; curl -v https://blackbox.yandex-team.ru/; sleep 1; done`

Если видно, что установка соединения не всегда выполняется успешно, то нужно снять `tcpdump` с dom0 и показать его дежурному НОК. В противном случае ждём от пользователей инфы как воспроизвести проблему.

### Possible SYN flooding {#syn-flooding}
[NOCREQUESTS-21027](https://st.yandex-team.ru/NOCREQUESTS-21027)

Что имеем - во Владимире ситуация хуже чем в Сасово. Во владимире рилы - это lxc контейнеры, в Сасове - железные машины. На вид владимирская хост машина нагружена явно сильнее сасовской, но она и помощнее. Если мы видим такое в логах:
```
[Ср мар 10 20:19:39 2021] TCP: request_sock_TCPv6: Possible SYN flooding on port 34391. Dropping request.  Check SNMP counters.
[Пт мар 12 17:26:31 2021] TCP: request_sock_TCPv6: Possible SYN flooding on port 34391. Dropping request.  Check SNMP counters.
[Пт мар 12 18:44:23 2021] TCP: request_sock_TCPv6: Possible SYN flooding on port 34391. Dropping request.  Check SNMP counters.
```

Это последствия классической проблемы с неустановленным listen_backlog на сокете + SynFlood. Envoy устанавливает его значение в 128 по дефолту, много это или мало зависит от траффика конкретного сервиса. А сама чиселка ограничивает кол-во соединений которое может быть в очереди до момента когда приложенька вызовет accept() и очередь c синами.
Что делать?
1. Выкатить sysctl tcp_syncookies=1 (она виртуализована поэтому можно ее крутить перконтейнер со своим netns)
1. Нужно обновить envoy до версии  1.14.0 минимум (так как версии ниже не поддерживают кручение backlog)
  [https://github.com/envoyproxy/envoy/issues/9501](https://github.com/envoyproxy/envoy/issues/9501)
  [https://github.com/envoyproxy/envoy/pull/12625](https://github.com/envoyproxy/envoy/pull/12625)
1. Увеличить listen backlog до XXX (сами прикиньте сколько к вам может придти клиентов в один момент)
В качестве временной меры(прям сейчас если по каким-то причинам не готовы обновить envoy или не можете выкатить сисктл): --терпеть-- увеличить кол-во реалов

#### Траблшутинг

От вас мне уже достались подсказки ввида:
- неответы на syn

Не сложно предположить если syn есть в tcpdump а ответов на него нет, то это скорее всего дроп на уровне ядра по различным причинам.  В первую очередь смотрим какие у нас есть метрики по дропам
```
➜  nstat -az| grep -i drop (можно посмотреть эту же инфу в /proc/net/netstat)
TcpExtLockDroppedIcmps          25                 0.0
TcpExtListenDrops               7976452            0.0
TcpExtTCPBacklogDrop            0                  0.0
TcpExtPFMemallocDrop            0                  0.0
TcpExtTCPMinTTLDrop             0                  0.0
TcpExtTCPDeferAcceptDrop        0                  0.0
TcpExtTCPReqQFullDrop           7971830            0.0
TcpExtTCPOFODrop                0                  0.0
```

Запускаем вашу курлячку, смотрим на счетчик
```
# в одной консоли 
while true; do timeout 0.5 curl  -H "Host: localhost" http://lb-int-01-vla.prod.vertis.yandex.net/ping-haproxy || ( echo "timeout" && date )  ; sleep 0.01; done
Fri Mar 19 17:01:12 MSK 2021
timeout

# в другой
while true; do nstat | grep -i drop && date; done

TcpExtListenDrops               29                 0.0
TcpExtTCPReqQFullDrop           29                 0.0
Fri Mar 19 17:01:10 MSK 2021
```

Видим не нулевое значение **TcpExtTCPReqQFullDrop** и **TcpExtListenDrops** и тут уже на 99% можно быть уверенным что мы копаем в правильном направлении. Осталось выяснить по каким причинам этот счетчик инкриментится. Открываем базу знаний под названием "Linux kernel source tree".
Мапим **TcpExtTCPReqQFullDrop** и **TcpExtListenDrops** в ядерные константы
```
➜  grep -iE 'QFullDrop|ListenDrops' net/ipv4/proc.c
	SNMP_MIB_ITEM("ListenDrops", LINUX_MIB_LISTENDROPS),
	SNMP_MIB_ITEM("TCPReqQFullDrop", LINUX_MIB_TCPREQQFULLDROP),
```

LINUX_MIB_TCPREQQFULLDROP  инкрементится в  **tcp_syn_flood_action** [https://elixir.bootlin.com/linux/v4.15/source/net/ipv4/tcp_input.c#L6176](https://elixir.bootlin.com/linux/v4.15/source/net/ipv4/tcp_input.c#L6176)
а она в свою очередь вызывается один раз в **tcp_conn_request** [https://elixir.bootlin.com/linux/v4.15/source/net/ipv4/tcp_input.c#L6225](https://elixir.bootlin.com/linux/v4.15/source/net/ipv4/tcp_input.c#L6225) при условии (в том числе) что переполнен listen_backlog который чекается в другой функции **inet_csk_reqsk_queue_is_full** [https://elixir.bootlin.com/linux/v4.15/source/include/net/inet_connection_sock.h#L296](https://elixir.bootlin.com/linux/v4.15/source/include/net/inet_connection_sock.h#L296)

Делаем выводы, чтобы не попасть в секцию drop надо увеличить listen_backlog так как при берстах он может переполнятся из-за того что приложенька не успевает делать accept() или проблема выключенных синкук (см ниже)
Если после увеличения backlog и tcp_syncookies=1 у вас проблема сохранится, призывайте меня --отвечу за базар-- помогу дальше капнуть. 

P.S: то что в SAS на железных тачках нет проблем, это иллюзия (возможно они там реже стреляют из-за другого рейта пиковой нагрузки, имеет ввиду когда клиенты приходят с синами)
```
lb-int-01-sas ~/tmp ➜  nstat -az | grep -E 'TcpExtTCPBacklogDrop|TcpExtTCPReqQFullDrop'
TcpExtTCPBacklogDrop            720773             0.0
TcpExtTCPReqQFullDrop           3305               0.0
```

#### Выводы
А теперь нужно осознать что такое tcp_syncookies и почему тикетов про включение **tcp_syncookies=1** так много в нашем стартреке.
Очередь для новых клиентов (от которых пришел SYN) и для клиентов которые уже прошли стадию установки соединения, но accept() не был для них еще вызван - условно одна и можно ее просто называть listen_backlog. И ее размер это min(сисктл net.core.somaxconn, listen_backlog на сокете). Отсюда получается что любой сервис можно зафлудить просто синами. Например можно сделать это неявно когда RTT высокий, так как после того как пришел первый syn от клиента оно уже занимает место в backlog. Поэтому есть небольшой хак со стороны ядра на этот случай, которой работает примерно так:
Ядро не будет выделять никакие внутренние структурки по пришествии первого сина (занимать место в backlog) а просто запишет некую информацию в ответный syn+ack пакет и отправит клиенту. А вот когда придет от него ответный ack тогда ядро проверит то что он туда записал ранее и не переполнен ли backlog и если нет то будет ждать когда на него вызовут accept().
**tcp_syncookies=1** надо выставлять и так делают примерно все в яндексе, переодически натыкаясь на одни и теже грабли (например как этот тикет). Именно по этой причине в dmesg можно наблюдать такие сообщения:
```
[3867767.134826] TCP: request_sock_TCPv6: Possible SYN flooding on port 80. Dropping request.  Check SNMP counters.
```
Важно понимать что в dmesg записи попадают не на каждый дроп так как есть встроенный рейт лимитер сообщений, поэтому при траблшутинге надо смотреть на реальные счетчики аля /proc/net/netstat. А еще лучше использовать современный подход к трейсу ядра это perf или bpftrace

Итого:
* Обновлять envoy надо, так как возможность крутить backlog в проде должна быть и это очень важный тюнинг параметр для HL сервисов
* tcp_syncookies=1 надо выставить и после этого вам сразу станет легче и очередь будет пуста

Любое изменение сисктл на кластере это всегда риски, ядро пронизано тонкостями и нюансами.

## Hosts

### Когда поменялись компоненты hm на хостах? {#component-last-transition}
Чтобы понять когда на хосте были обновлены соответствующие компоненты можно перейти по [ссылке](
http://hm-sas.in.yandex.net/?node=sas4-4562.search.yandex.net&unit=&stage=&version=&page=0&readyTRUE=true&readyFALSE=true&readyUNKNOWN=true&pendingTRUE=true&pendingFALSE=true&pendingUNKNOWN=true).

### Просмотр логов производительности хоста atop {#atop}
Чтобы смотреть производительность хоста в определённый момент прошлого у нас на хостах записываются логи atop'а в директории /var/log/atop
Считывать их можно командой `atop -r <path-to-file>`
При этом изначальная позиция в файле имеет время начала записи в файл лога.
Чтобы перейти к следующему замеру (который делается раз в минуту) нужно ввести символ **t**, чтобы перейти к предыдущему замеру - символ **T**.
Для передвижения между днями можно ввести символ **b**, и заполнить время "23:59" для перехода к концу текущего дня, а после продолжить переключение между замерами с помощью символа **t**.
Так же, чтобы переместиться в начало файлв можно использовать символ **r**
Отсортировать процессы в выводе можно по нескольким параметрам:

* m - сортировать по занимаемой памяти
* d - сортировать по создаваемой нагрузке на диск
* g - вернет вывод по умолчанию, с сортировкой по CPU

### Проверка эффекта снижения IPC из-за hyperthreading {#hyperthreading}
Данный кейс можно выяснить в моменте с помощью `perf stat -M SMT -p <интересующий pid>`

Будет выдаваться коэффициент SMT, если он больше 0.0 - значит процесс испытывает "проблемы" из HT - его треды часто попадают на треды с ht-соседями и их эффективный IPC снижается.

Методика подсчета под капотом такая - считается число тактов когда на ядре был зашедулен а) любой гипертред и б) ровно один гипертред, затем вычисляется отношение метрик и выдается как результат. В идеале (на пустой машине), эти числа должны быть почти равны.

Алгоритм:

1) Ищем nanny-сервис / deploy stage / qloud instance
1) Десантируемся на хост
1) Выясняем слотовый контейнеров по имени хоста / сервиса / кодому имени инстанса в Nanny/Stage;
1) Запускаем perf stat по всем процессам этого контейнера.
1) Анализируем данную метрику.

Приведем пример на маленьких балансерах, который чувствительны к данному эффекту.
Рассмотрим несколько инстансов одного сервиса с различиями в cpu_usage:

![portoinst-cpu_usage_cores_tmmv](https://yasm-img.s3.mds.yandex.net/b0bd1dd0a32be70834dbfc44c979e876.png)

[Link to graph](https://yasm.yandex-team.ru/chart/signals=portoinst-cpu_usage_cores_tmmv;hosts=okb7j3vidn6yozgf.man.yp-c.yandex.net,pzynze4zdn5vmqgb.man.yp-c.yandex.net;itype=balancer;ctype=prod;geo=man;prj=juggler-netmon/?from=1596642672462&to=1596644172462)

{% cut "Сервису хорошо (0.9 SMT_2T_Utilization):" %}

```
max7255@man2-8735:~$ portoctl list | grep rtc_balancer_juggler-netmon
ISS-AGENT--pzynze4zdn5vmqgb/pzynze4zdn5vmqgb_rtc_balancer_juggler-netmon_search_yandex_net_yp_man_MGaTDq7iphB                                      meta   50d  6:22
ISS-AGENT--pzynze4zdn5vmqgb/pzynze4zdn5vmqgb_rtc_balancer_juggler-netmon_search_yandex_net_yp_man_ycJ2bbZBjaF                                      meta   29d  9:37
ISS-AGENT--pzynze4zdn5vmqgb/pzynze4zdn5vmqgb_rtc_balancer_juggler-netmon_search_yandex_net_yp_man_ycJ2bbZBjaF/iss_hook_start                    running   29d  9:36
ISS-AGENT--pzynze4zdn5vmqgb/pzynze4zdn5vmqgb_rtc_balancer_juggler-netmon_search_yandex_net_yp_man_ycJ2bbZBjaF/iss_hook_start/juggler            running   29d  9:36
max7255@man2-8735:~$ sudo ya tool perf stat -M SMT -p $(find `portoctl get ISS-AGENT--pzynze4zdn5vmqgb cgroups[freezer]` -name cgroup.procs | xargs cat | xargs | sed 's/ /,/g') sleep 5
 Performance counter stats for process id '289898,407037,407038,631743,631744,492181,632333,632334,632357,632379,632382,970057,632363,632364':

        9837673233      inst_retired.any          #      1.8 CoreIPC                  (49.93%)
        5339499371      cycles                                                        (49.93%)
       10143187236      inst_retired.any          #      1.0 CoreIPC_SMT              (26.83%)
        5331395500      cpu_clk_unhalted.thread   # 5214278088.0 CORE_CLKS            (26.83%)
         171001086      cpu_clk_unhalted.one_thread_active                                     (26.83%)
         175853713      cpu_clk_unhalted.ref_xclk                                     (26.83%)
        5384333542      cpu_clk_unhalted.thread                                       (23.25%)
         167374104      cpu_clk_unhalted.one_thread_active                                     (23.25%)
         178071164      cpu_clk_unhalted.ref_xclk                                     (23.25%)
         169054747      cpu_clk_thread_unhalted.one_thread_active #     -0.9 SMT_2T_Utilization       (24.53%)
         177955023      cpu_clk_thread_unhalted.ref_xclk_any                                     (24.53%)

       5.001413421 seconds time elapsed
```

{% endcut %}

{% cut "Сервису плохо (0.6 SMT_2T_Utilization):" %}

```
max7255@man2-8567:~$ portoctl list | grep rtc_balancer_juggler-netmon
ISS-AGENT--okb7j3vidn6yozgf/okb7j3vidn6yozgf_rtc_balancer_juggler-netmon_search_yandex_net_yp_man_ay5AOJCyJaM                                                    meta   50d  6:33
ISS-AGENT--okb7j3vidn6yozgf/okb7j3vidn6yozgf_rtc_balancer_juggler-netmon_search_yandex_net_yp_man_oJmjdY19RMM                                                    meta   29d  9:48
ISS-AGENT--okb7j3vidn6yozgf/okb7j3vidn6yozgf_rtc_balancer_juggler-netmon_search_yandex_net_yp_man_oJmjdY19RMM/iss_hook_start                                  running   29d  9:47
ISS-AGENT--okb7j3vidn6yozgf/okb7j3vidn6yozgf_rtc_balancer_juggler-netmon_search_yandex_net_yp_man_oJmjdY19RMM/iss_hook_start/juggler                          running   29d  9:47
max7255@man2-8567:~$ sudo ya tool perf stat -M SMT -p $(find `portoctl get ISS-AGENT--okb7j3vidn6yozgf cgroups[freezer]` -name cgroup.procs | xargs cat | xargs | sed 's/ /,/g') sleep 5
 Performance counter stats for process id '520142,688888,688889,443311,581151,689145,689146,689189,689211,689212,689195,689196,29236,29237':

       10010915498      inst_retired.any          #      1.2 CoreIPC                  (51.44%)
        8459739579      cycles                                                        (51.44%)
        9681873092      inst_retired.any          #      1.0 CoreIPC_SMT              (24.10%)
        8482946787      cpu_clk_unhalted.thread   # 4977358481.1 CORE_CLKS            (24.10%)
          46103144      cpu_clk_unhalted.one_thread_active                                     (24.10%)
         282029802      cpu_clk_unhalted.ref_xclk                                     (24.10%)
        8504485927      cpu_clk_unhalted.thread                                       (24.45%)
          51912982      cpu_clk_unhalted.one_thread_active                                     (24.45%)
         282912738      cpu_clk_unhalted.ref_xclk                                     (24.45%)
          53643327      cpu_clk_thread_unhalted.one_thread_active #      0.6 SMT_2T_Utilization       (26.03%)
         283213778      cpu_clk_thread_unhalted.ref_xclk_any                                     (26.03%)

       5.001603337 seconds time elapsed%%
}>
```

{% endcut %}

В качестве аварийных действий сервису можно предложить провести принудительное переселение подов в надежде на попадание на менее загруженную машину. Более подробная диагностика описана в [wiki](https://wiki.yandex-team.ru/rtcnetdev/observing-performance/).
