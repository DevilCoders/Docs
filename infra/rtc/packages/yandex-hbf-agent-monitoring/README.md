# Скрипты мониторинга yandex-hbf-agent'а
В этом пакете находятся скрипты пассивных Juggler-проверок yandex-hbf-agent'а.

## Базовая juggler-проверка - hbf-monitoring

Данная проверка содержит в себе ряд отдельных функций для проверки наличия
пакета на хосте, запущенного процесса и т.п. Некоторые из них по умолчанию
выключены т.к. используюстя только в Рантайм облаке и другим проектам особо не
нужны. Список функций:

<table>
    <tr>
        <td>Название</td>
        <td>Описание</td>
        <td>Включена по умолчанию</td>
    </tr>
    <tr>
        <td><code>check_package</code></td>
        <td>проверяет состояние пакета <code>yandex-hbf-agent</code></td>
        <td>✓</td>
    </tr>
    <tr>
        <td><code>check_process</code></td>
        <td>проверяет состояние процесса <code>yandex-hbf-agent</code></td>
        <td>✓</td>
    </tr>
    <tr>
        <td><code>check_status</code></td>
        <td>проверяет значения возвращаемые ручкой <code>/status</code></td>
        <td>✓</td>
    </tr>
    <tr>
        <td><code>check_br_netfilter</code></td>
        <td>проверяет наличие бриджей и загрузку модуля
            <code>br_netfilter</code></td>
        <td>✓</td>
    </tr>
    <tr>
        <td><code>check_notrack</code></td>
        <td>проверяет наличие правил <code>NOTRACK</code> для TCP соединений
            (используется в Рантайме)</td>
        <td>❌</td>
    </tr>
    <tr>
        <td><code>check_protected_chains</code></td>
        <td>проверяет, что защищённые цепочки не удалялись агентом в
            последнее время (используется в Рантайме)</td>
        <td>❌</td>
    </tr>
</table>

```
$ hbf-monitoring -h
usage: check HBF agent [-h] [--without-package] [--without-process]
                       [--without-status] [--without-br-netfilter]
                       [--with-notrack] [--with-protected-chains]

optional arguments:
  -h, --help            show this help message and exit
  --without-package     disable check 'check_package'
  --without-process     disable check 'check_process'
  --without-status      disable check 'check_status'
  --without-br-netfilter
                        disable check 'check_br_netfilter'
  --with-notrack        enable check 'check_notrack'
  --with-protected-chains
                        enable check 'check_protected_chains'
```

## Juggler-проверка количества дропов пакетов - hbf-monitoring-drops
### Как пользоваться:
```
$ hbf-monitoring-drops -h
usage: hbf-monitoring-drops [-h] [-c LIMITS_CONFIG_FILE] [-p HISTORY_FILE]
                            [-l MAX_HISTORY_RECORDS] [-r NEW_PROBES_NUM] [-d]
                            [-m] [-o] [-z] [--v4-input TOTAL DROPPED]
                            [--v4-output TOTAL DROPPED]
                            [--v6-input TOTAL DROPPED]
                            [--v6-output TOTAL DROPPED]

HBF drops monitoring tool.

optional arguments:
  -h, --help            show this help message and exit
  -c LIMITS_CONFIG_FILE, --limits-config-file LIMITS_CONFIG_FILE
                        Path to config file with limits
  -p HISTORY_FILE, --history-probes-file HISTORY_FILE
                        Path to previous probes file
  -l MAX_HISTORY_RECORDS, --history-len MAX_HISTORY_RECORDS
                        Number of items stored in history
  -r NEW_PROBES_NUM, --ratio-burst-new-num NEW_PROBES_NUM
                        Number of items which are treated as 'new'
  -d, --debug           Print probes analysis info
  -m, --manual-counters
                        Provide counters from command line, see below
  -o, --off-no-data-alarm
                        No data is OK. CRIT by default.
  -z, --prelog-hook-zero-drop
                        Not count drops inside PRELOG_HOOK chain.
  --v4-input TOTAL DROPPED
  --v4-output TOTAL DROPPED
  --v6-input TOTAL DROPPED
  --v6-output TOTAL DROPPED

```
Параметры по умолчанию:
```
DEFAULT_LIMITS_CONFIG_FILE = "/etc/yandex-hbf-agent/drops-monitoring-config.yaml"
DEFAULT_HISTORY_FILE = "/var/tmp/hbf-monitoring-drops-history.tmp"
DEFAULT_MAX_HISTORY_RECORDS = 12
DEFAULT_NEW_PROBES_NUM = 3
```

### Принцип работы

Скрипт снимает счетчики количества пакетов, попавших в цепочки
```
Y_FW        # INPUT, начальная цепочка HBF'а
Y_END_IN    # INPUT, конечная цепочка HBF'а с правилами DROP и/или LOG
Y_FW_OUT    # OUTPUT, начальная цепочка HBF'а
Y_END_OUT   # OUTPUT, конечная цепочка HBF'а с правилами REJECT и/или LOG
```
, командами типа `sudo -n ip6tables -vS Y_FW`.
Данные собираются для IPv4 и IPv6.
За "количество пакетов, попавших в цепочку", принимается:
* для INPUT - сумма значений всех счетчиков правил
* для OUTPUT - сумма счетчиков правил LOG или DROP/REJECT (максимум из них - бывают только логи без DROP)
Если запрошенной цепочки нет, или если значения счетчиков не удалось
распарсить - сохраняется `Null`.


Полученный набор значений счетчиков + текущий timestamp - это "проба". Скрипт
ведет файл истории `HISTORY_FILE`, в котором хранится максимум
`MAX_HISTORY_RECORDS`, собственно, проб. После получения текущего
значения счетчиков файл проб обновляется, самая новая добавленная проба
вытесняет самую старую.


Допустим, у нас есть 12 проб (текущих значений счетчиков) [p1, p2, .., p12].
Значит, полезных значений, которыми мы можем оперировать, у нас 11, так как мы
смотрим на динамику изменения счетчиков, а не на их абсолютные значения. Назовем
эти полезные значения [v1, v2, ..., v11]. v, очевидно, вычисляются так:
```
v1["v6"]["input"]["packets_total"] = \
    p2["v6"]["input"]["packets_total"] - p1["v6"]["input"]["packets_total"]
...
v11["v6"]["input"]["packets_total"] = \
    p12["v6"]["input"]["packets_total"] - p11["v6"]["input"]["packets_total"]
```
для каждого из `["v4", "v6"]`, `["input", "output"]`,
`["packets_total", "packets_dropped"]`.

При вычислении v работают следующие умолчания:
* игнорируются (пропускаются) пробы без значений счетчиков (iptables затупил,
  счетчики не получилось выпарсить). Количество полезных значений при этом,
  очевидно, сокращается на 1.
* если значение счетчика было сброшено между пробами (значение текущей пробы
  меньше чем предыдущей), за разницу принимается значение текущей пробы.


Затем **по всем имеющимся полезным значениям** `[v1, v2, ..., v11]` вычисляется
несколько параметров:
* `drops_per_second` - количество дропов в секунду.
* `summ_packets_dropped` - сумма дропнутых пакетов.
* `max_packets_dropped` - максимальное значение количество дропнутых пакетов
  среди всех [v1, v2, ..., v11].
* `dropped_total_ratio` - соотношение "дропнутые/входящие".
* `ratio_average_increase` - тут стоит пояснить подробнее.
  1. Вычисляется 11 соотношений "дропнутые/входящие", за каждый из периодов
     [v1, v2, ..., v11]. Назовем их [r1, r2, ..., r11]. r1 - самое старое,
     r11 - самое новое.
  2. Параметр `NEW_PROBES_NUM` задает нам количество "новых" соотношений,
     по умолчанию "3".
  2. Вычисляется медиана `[r1, r2, .., r8]` (среднее значение соотношения
     "дропнутые/входящие" по "старым" пробам), назовем ее `m_old`.
  3. Вычисляется медиана `[r9, r10, r11]` (среднее значение соотношения
     "дропнутые/входящие" по "новым" пробам), назовем ее `m_new`.
  4. `ratio_average_increase` = `m_new / m_old`.
  Также действуют следующие умолчания:
  1. Если количество "старых" проб меньше количества "новых", то
     `ratio_average_increase = 0.0`.
  2. Если `m_new == 0` или `m_old == 0`, то `ratio_average_increase = 0.0`.


### Установка лимитов на `WARN` и `CRIT`
Итак, после каждого запуска скрипта у нас имеется ряд параметров, вычисленных
за весь период сохранения истории. Собственно мониторинг заключается в сравнении
вычисленных параметров с заданными лимитами на эти параметры. Лимиты задаются в
конфигурационном файле `LIMITS_CONFIG_FILE`, формат файла - YAML.
Выглядеть он может, например, так:
```
# Some comment
v6:
    input:
        drops_per_second:
            in_use: False
            WARN: 0.01
            CRIT: 0.1
        summ_packets_total:
            in_use: True
            WARN: 10
            CRIT: 50
        max_packets_dropped:
            in_use: True
            WARN: 5
            CRIT: 30
    output:
        dropped_total_ratio:
            in_use: True
            WARN: 0.001
            CRIT: 0.05
v4:
    output:
        ratio_average_increase:
            in_use: True
            WARN: 6.0
            CRIT: 10.0
```

При `MAX_HISTORY_RECORDS = 12` и запуске Juggler-проверки каждые 5 минут, смысл
параметров становится таким:
`drops_per_second` - в течение прошедшего часа в секунду дропалось `> 0.1`
пакета
`summ_packets_total` - в течение прошедшего часа всего дропнулось `> 50` пакетов
`max_packets_dropped` - в течение прошедшего часа был 5-минутный период, за
который дропнулось `> 30` пакетов.
`dropped_total_ratio` - за прошедший час итоговое соотношение
"дропнутые / пришедшие в цепочку" составило `> 0.05`.
`ratio_average_increase` - среднее соотношение дропов за последние 15 минут
больше среднего соотношения дропов за предыдущие 45 минут в `10` раз.

Дополним каждое выражение словами "по IPv4 в INPUT" например, это понятно из
структуры конфигурационного файла.
Флажок `in_use: [True | False]` активирует или, соответственно, деактивирует
этот лимит.
Наличие блоков каждого из уровней необязательно.

Результат всей Juggler-проверки - `CRIT`, если хоть один из указанных и
in_use-параметров вычислился в `CRIT`, то же самое для `WARN`. `CRIT` имеет
больший приоритет, чем `WARN`. Каждый из лимитов, если он превышен, дополняет
собой строку description'а проверки, например:
```
PASSIVE-CHECK:hbf_drops;2;v6-input-drops_per_second > 0.1; v6-output-dropped_total_ratio > 0.001
```

### Самомониторинг
Если в конфигурационном файле заданы параметры, например для `v4: output:`, а
сырых данных для этой комбинации нет вообще - проверка загорится в `CRIT`, и
описание дополнится строчкой `v4-output no data at all`. Переопределить это
поведение можно ключом `-o, --off-no-data-alarm`: если он есть, отсутствие
данных не повлечет зажигание `CRIT` (но description все равно дополнится).

Если конфигурационный файл `LIMITS_CONFIG_FILE` невозможно прочитать как
YAML - загорится `CRIT`. Это сделано специально, чтобы исключить молчание
мониторинга в случае "забыли положить конфиг". Дефолтных значений лимитов нет.

Если файл с историей проб `HISTORY_FILE` не удалось прочитать как JSON -
загорится `CRIT`. При первоначальной установке пакета этот `CRIT` также
загорится, но на следующей итерации потухнет, это тоже нормально и сделано для
безопасности.

Если файл с историей проб `HISTORY_FILE` не удалось записать - загорится `CRIT`.


### Режим отладки
Если в командной строке задан ключ `--debug`, скрипт
1. Не будет дополнять историю текущим значением счетчиков.
2. Выдаст в stdout результаты анализа истории, например такие:
   https://paste.yandex-team.ru/222616 .

Для отладки скрипт также поддерживает передачу значений счетчиков вручную. При
задании ключа `-m` текущее значение счетчиков берется не из iptables, а из
параметров навроде
```
hbf-monitoring-drops -m \
    --v4-input 100 1
    --v6-output 200 0
```
где `100` - это количество пакетов, попавших в начальную цепочку, а `1` -
количество дропнутых пакетов. Значения счетчиков не указанных ключей -
`[Null, Null]`, что эмулирует сломавшийся iptables или отсутствие
соответствующих цепочек. Стоит понимать, что числа здесь - это абсолютные
значения счетчиков, а не то, насколько они изменились.
Имея эти инструменты, можно организовать тестирование логики скрипта примерно
так:
```
t=100; d=0; \
for i in `seq 1 12`; do \
    echo $t $d; \
    hbf-monitoring-drops -m --v6-input $t $d; \
    t=$((t + 100)); d=$((RANDOM%5+d)); \
    sleep 5; \
done; \
hbf-monitoring-drops --debug
```


## Рисовалка графиков дропов пакетов для Graphite - hbf-monitoring-drops-graphite
### Как пользоваться:
```
$ hbf-monitoring-drops-graphite -h
usage: hbf-monitoring-drops-graphite [-h] [-d HISTORY_FILE] [-t TIME_PREFIX]
                                     [-f FQDN] [-p POSTFIX] [-o OUTPUT_STYLE]

HBF drops Graphite collector.

optional arguments:
  -h, --help            show this help message and exit
  -d HISTORY_FILE, --previous-data HISTORY_FILE
                        Path to file with previous data
  -t TIME_PREFIX, --time-prefix TIME_PREFIX
                        Graphite time period prefix
  -f FQDN, --fqdn FQDN  This server's FQDN in Graphite format
  -p POSTFIX, --postfix POSTFIX
                        Postfix, under which metrics data will be stored
  -o OUTPUT_STYLE, --output-style OUTPUT_STYLE
                        Output style, can be "default" or "simple". For
                        "simple" style output POSTFIX used as PREFIX and has
                        no TS in output.

```
Параметры по умолчанию:
```
DEFAULT_GRAPHITE_HISTORY_FILE = "/var/tmp/hbf-monitoring-drops-graphite.tmp"
DEFAULT_GRAPHITE_TIME_PREFIX = "one_min"
DEFAULT_GRAPHITE_FQDN = getfqdn().replace('.', '_')
DEFAULT_GRAPHITE_POSTFIX = "hbf"
DEFAULT_GRAPHITE_OUTPUT_STYLE = "default"
```

### Принцип работы

Скрипт снимает счетчики количества пакетов, попавших в цепочки
```
Y_FW        # INPUT, начальная цепочка HBF'а
Y_END_IN    # INPUT, конечная цепочка HBF'а с правилами DROP и/или LOG
Y_FW_OUT    # OUTPUT, начальная цепочка HBF'а
Y_END_OUT   # OUTPUT, конечная цепочка HBF'а с правилами REJECT и/или LOG
```
, командами типа `ip6tables -L Y_FW -n -v -x -w`.
Данные собираются для IPv4 и IPv6.
За "количество пакетов, попавших в цепочку", принимается:
* для INPUT - сумма значений всех счетчиков правил
* для OUTPUT - максимальное значение среди счетчиков правил LOG или DROP/REJECT
Если запрошенной цепочки нет, или если значения счетчиков не удалось
распарсить - сохраняется `Null`.


Полученный набор значений счетчиков + текущий timestamp - это "проба". Скрипт
ведет файл истории `GRAPHITE_HISTORY_FILE`, в котором хранит предыдущую пробу.
После получения текущего значения счетчиков файл проб обновляется.
Скрипт выплевывает разницу между значениями счетчиков текущей и предыдущей пробы
в graphite-совместимом формате, типа
```
one_min.server_yandex_net.hbf.v4.input.packets_dropped 42 1492094569
```
Если значение счетчика в предыдущей пробе больше, чем в текущей (счетчики
сбросились) - за разницу берется значение текущей пробы.
Если значение счетчика в текущей или предыдущей пробе не удалось определить, то
разница не вычисляется, на графике будет "дырка".
