# Нагрузочное тестирование L3 балансировщиков

Данный документ описывает процесс нагрузочного тестирования L3 балансировщиков на базе как IPVS, так и YANET.

## Стенд

Стенд представляет из себя следующий набор машин во Владимирской лабе:
- Танки - генераторы нагрузки, как HTTP так и UDP в зависимости от конфигурации.
- L3 - два L3 балансировщика с разными бекендами.
- Список рилов, которые обслуживают нагрузку.
- Два фаерволла, через которые пропускается обратный трафик.

![](scheme.svg)

На схеме, чтобы не нагромождать ее, не показаны пути трафика от фаерволлов до танков.

## Танк
Один танк из себя представляет обычную железную машину, на которую ставится генератор нагрузки. При этом требования к
генератору специфические:
- Он должен уметь генерировать максимально большую нагрузку HTTP запросами. Под **большой** мы понимаем минимум 3 миллиона RPS с одной машины. Больше - лучше.
- Помимо HTTP также должна быть возможность генерировать UDP пакеты. Тут требования к рейту запросов еще больше - до 8-10 миллионов пакетов у секунду с одной машины.
- Возможность кастомизации нагрузки - любой HTTP body и набор заголовков.
- Для тестирования распухания хеш-таблиц должна быть возможность принудительно устраивать пересоздание сокетов после N запросов.
- Должна иметься возможность биндиться на несколько IP адресов.
- Возможность настраивать профили нагрузки: константа, линия, любой другой профиль. :)
- Танк должен уметь считать метрики по кол-ву пакетов, статусов ответов, квантили времен ответов.
- Метрики должны иметь возможность аггрегации с нескольких машин в один график. Идеально - отправлять в Соломон.

Существующие решения по генерации нагрузки не подходят по ряду причин:
- Yandex.Tank - слишком медленный (как phantom, так и pandora). В остальном - подходит.
- wrk - по производительности устраивает. В остальном - нет.

Поэтому был написан свой специализированный генератор нагрузки. Название - bang, запакетирован, пакет лежит под таким же названием в debian репозитории noc.

### Bang
Bang представляет из себя высокопроизводительный и одновременно гибкий (под наши нужды) генератор трафика. Он позволяет
генерировать как HTTP, так и UDP запросы, утилизируя машину по-максимуму.

Работает он следующим образом.
Запускается столько потоков, сколько указано в опции (если не указано, то берется кол-во логических ядер на системе), при этом в каждом из них запускается определенное количество асинхронных задач (a-la корутин) таким образом, чтобы их суммарное количество было равным параметру `concurrency`.
Каждая асинхронная задача в цикле старается сгенерировать запросы таким образом, чтобы уложиться в профиль нагрузки.
Также стоит отметить, что еще до запуска каждая асинхронная задача выбирает себе bind IP адрес и запросы будут идти только с него. Порты выбираются рандомно из свободных. Если число возможных IP адресов меньше, чем задач, то некоторые из них переиспользуются.
Для поддержания профиля нагрузки используется алгоритм [Leaky Token Bucket](https://en.wikipedia.org/wiki/Leaky_bucket).
Существует возможность бёрстов.

Если указана опция `--requests-per-socket=N`, то каждые `N` запросов сокет пересоздается. Порт выбирается из свободных операционной системой. 

Присутствует встроенное описание:
```
bang 0.1.0
Evgeny Safronov <esafronov@yandex-team.ru>
High performance traffic generator

USAGE:
    bang [OPTIONS] <URI>

ARGS:
    <URI>    URI to bang

OPTIONS:
    -t, --threads <THREADS>
            Number of threads [default: 80]

    -c, --concurrency <CONCURRENCY>
            Number of parallel coroutines. This also limits the maximum concurrent requests in
            flight. To achieve better runtime characteristics this value should be the multiple of
            the number of threads [default: 1600]

    -H, --header <HEADERS>
            Extra HTTP headers. By default no HTTP headers (even Host) are specified to the payload.
            However sometimes it is necessary to provide additional headers

        --bind-ips <BIND_IPS>
            Path to the file with IP addresses to bind. If none given (default) the "::" bind
            address will be used unless "bind_network" argument is provided

        --bind-network <BIND_NETWORK>
            IP prefix used to collect this machine's global unicast IP addresses and use them as
            bind addresses. For example, specifying "2a02:6b8:0:320:1111:1111:1111::/112" will scan
            all interfaces, collect all global unicast IP addresses and filter them by the given
            prefix

        --requests-per-socket <REQUESTS_PER_SOCKET>
            Requests per socket before reconnection

        --linger <LINGER>
            Set linger TCP option with specified value

        --no-delay
            Configure SOCK_NODELAY socket option

        --mode <MODE>
            Load testing mode [default: http] [possible values: http, udp, udp-rpc]

        --generator <GENERATOR>
            Path to the generator file. See /etc/bang/generator.yaml for details

        --generator-stdin
            Take generator profile from stdin as line separated values

        --no-ui
            Disable terminal UI

        --no-solomon
            Disable pushing metrics to Solomon

        --solomon-base-uri <SOLOMON_BASE_URI>
            Solomon base URI [default: https://solomon.yandex.net/api/v2/push]

        --solomon-project <SOLOMON_PROJECT>
            Solomon project [default: noc]

        --solomon-cluster <SOLOMON_CLUSTER>
            Solomon cluster [default: all]

        --solomon-service <SOLOMON_SERVICE>
            Solomon service [default: tank]

    -v
            Be verbose in terms of logging

    -h, --help
            Print help information

    -V, --version
            Print version information
```

Код располагается [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/junk/esafronov/bang).

### Профили нагрузки
Профили нагрузки задаются отдельно в виде YAML файлов, которые имеют следующую структуру:
```yaml
type: seq
generators:
  - type: line
    rps: [0, 1000000]
    duration: 60
  - type: sin
    pps: [1000000, 1000000]
    pps_min: 500000
    pps_max: 2500000
    approximate_period: 30
    duration: 60
  - type: const
    rps: 1000000
    duration: 60
  - type: line
    rps: [1000000, 5000000]
    duration: 240
```

Почти в каждом типе генератора, кроме `seq` и `sum` (которые являются аггрегационными), обязателен параметр `duration`, который говорит, сколько секунд должна генерироваться нагрузка.

Поддерживаются следующие типы генераторов:
- const - держит указанную константную нагрузку. Пример конфигурации:
  ```yaml
  type: const
  rps: 1000000
  duration: 60
  ```
- line - линейная функция, который монотонно возрастает или убывает на указанном промежутке `rps`. Самый часто используемый тип профиля, и, наверное, самый полезный.
  Пример конфига, в котором нагрузка возрастает от 0 до 5'000'000 RPS в течение 5 минут (300 сек):
  ```yaml
  type: line
  rps: [0, 5000000]
  duration: 300
  ```
- sin - синусоидальная функция. Тут немного посложнее, поскольку задавать синус в чистом виде не удобно с точки зрения граничных условий, особенно когда они ненулевые.
  Иначе говоря, сложно заранее предсказать, на каком RPS начнется и на каком закончится профиль при указанном времени.
  Поэтому задание профиля нагрузки осуществляется путем задания граничным условий, минимального и максимального RPS, из которых вычисляется амплитуда, и примерного периода.
  Настоящий период вычисляется аналитически в момент инициализации генератора.
  Пример профиля:
  ```yaml
  type: sin
  pps: [1000000, 1000000]
  pps_min: 500000
  pps_max: 2500000
  approximate_period: 30
  duration: 60
  ```
- seq - объединение нескольких генераторов в цепочку. Описывается как комбинация генераторов других типов. Допускается любой уровень вложенности.
  При этом суммарное время работы генератора эквивалентно сумме времен работы каждого вложенного генератора. 
  Пример, где сначала нагрузка растет линейно, потом держится на заданном уровне, а потом убывает до нуля:
  ```yaml
  type: seq
  generators:
  - type: line
    rps: [0, 2000000]
    duration: 60
  - type: const
    rps: 2000000    
    duration: 60
  - type: line
    rps: [2000000, 0]
    duration: 60
  ```
- sum - объединение нескольких генераторов в сумму. Полезно, когда необходимы более сложные профили нагрузки. При этом теоретически можно описать вообще любой профиль из суммы синусов, путем разложения изначальной функции в ряд Фурье.
  Суммарное время работы генератора вычисляется как максимальное время работы вложенных генераторов.
  При этом не обязательно подгонять параметр `duration` - если один из вложенных генераторов закончил работу, то будет считаться, что он генерирует ноль.
  Значения суммы меньше нуля автоматически становятся нулем.
  Пример суммы двух синусов разной частоты:
  ```yaml
  type: sum
  generators:
  - type: sin
    pps: [1000000, 1000000]
    pps_min: 500000
    pps_max: 1500000
    approximate_period: 60
    duration: 600
  - type: sin
    pps: [500000, 500000]
    pps_min: 250000
    pps_max: 1500000
    approximate_period: 10
    duration: 600
  ```
  
### Пример запуска
Итак, допустим мы хотим пострелять по цели `[2a02:6b8:0:3400:0:853a:0:5]:80` HTTP нагрузкой с 400 IP адресов с профилем от 0 до 5'000'000 за 300 секунд.
Что для этого надо?

Для начала, установить Debian пакет `bang`, который лежит в репозитории `noc`. Он привозит за собой как сам танк, так и `systemd` юнит для инициализации окружения.

Далее, убедиться, что такое кол-во адресов присутствует на машине. Имя интерфейса может меняться от машины к машине, поэтому для примера рассмотрим один из танков:
```bash
esafronov@lab-vla-srv4:~$ ip a show dev eth2
4: eth2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 8950 qdisc mq state UP group backbone qlen 1000
    link/ether 0c:42:a1:5a:30:50 brd ff:ff:ff:ff:ff:ff
    inet6 2a02:6b8:c0e:1003:0:675:ffff:190/64 scope global
       valid_lft forever preferred_lft forever
    inet6 2a02:6b8:c0e:1003:0:675:ffff:18f/64 scope global
       valid_lft forever preferred_lft forever
    inet6 2a02:6b8:c0e:1003:0:675:ffff:18e/64 scope global
       valid_lft forever preferred_lft forever
    inet6 2a02:6b8:c0e:1003:0:675:ffff:18d/64 scope global
       valid_lft forever preferred_lft forever
    inet6 2a02:6b8:c0e:1003:0:675:ffff:18c/64 scope global
    ...
    inet6 2a02:6b8:c0e:1003:0:675:ffff:2/64 scope global
       valid_lft forever preferred_lft forever
    inet6 2a02:6b8:c0e:1003:0:675:ffff:1/64 scope global
       valid_lft forever preferred_lft forever
    inet6 2a02:6b8:c0e:1003:0:675:a15a:3050/64 scope global
       valid_lft forever preferred_lft forever
    inet6 fe80::e42:a1ff:fe5a:3050/64 scope link
       valid_lft forever preferred_lft forever
```

Если по какой-то причине адресов нет или мало - следует их создать:
```bash
systemctl start bang-init
```

В случае, если стрельбы ведутся в не-лабном окружении, то можно воспользоваться грубой альтернативой:
```bash
python3 -c "print('\n'.join(f'{v:x}' for v in range(1, 401)))" | xargs -I {} sudo ip a add 2a02:6b8:c0e:1003:0:675:ffff:{}/64 dev eth2
```

{% note alert %}

Это потенциально опасная операция, т.к. может сделать плохо свитчу, в которую воткнута ваша машина.
Если не уверены, что делаете - лучше проконсультироваться с владельцем машины и сетевыми инженерами.

{% endnote %}

Надо убедиться, что локальный HBF агент (при его наличии) пропускает исходящий трафик.
Также стоит заранее убедиться, что фаерволл на L3 балансировщике корректно настроен, и что он не будет дропать входящий трафик.
Это настраивается по-разному в зависимости от типа L3 балансировщика.

{% note %}

Для отправки метрик танка в Соломон в environment должен быть проставлен OAuth токен:
```bash
export SOLOMON_OAUTH_TOKEN=AQAD-AAAABBBBCCCCDDDD
```

{% endnote %}

Также скорее всего надо будет поднять лимит открытых файловых дескрипторов:
```bash
ulimit -n 10000
```

Если все настроено корректно, то запускаем стрельбы и ждем их конца. При этом по-умолчанию отрисовывается консольный UI, который можно отключить опцией `--no-ui`.

Итак, стреляем с 80 ядер параллельно не более чем 1600 запросов до цели `http://[2a02:6b8:0:3400:0:853a:0:5]:80/`, при этом используем в качестве source IP адресов все, что есть локально и ложится в сеть `2a02:6b8:0:320:1111:1111:1111::/112`.
Каждые 36 запросов пересоздаем сокет.

В качестве генератора используем:
```yaml
type: seq
generators:
  - type: line
    rps: [0, 5000000]
    duration: 300
```

Погнали:
```bash
esafronov@lab-vla-yanet1:~/code/bang$ bang -t80 -c 1600 http://[2a02:6b8:0:3400:0:853a:0:5]:80/ --bind-network=2a02:6b8:0:320:1111:1111:1111::/112 --requests-per-socket=36 --generator ./etc/bang/generator.yaml
2022-01-25 10:05:08,987 INFO [bang::app] using 687 local IP addresses
2022-01-25 10:05:08,987 INFO [bang::app] watch your results at: https://grafana.yandex-team.ru/d/mUC6MG0nk/yanet-l3-tank
2022-01-25 10:05:08,987 INFO [bang::app] using 18 byte(s) ammo
2022-01-25 10:05:08,993 WARN [bang::app] no Solomon OAuth token provided in SOLOMON_OAUTH_TOKEN, pushing is disabled
Requests:
  planned : 1975188
  RPS     : 1975075 (max 1975075)
  summary : 117043328
  timeouts: 0
Transfer:
  tx: 284.162 Mbit/s
  rx: 2.086 Gbit/s
HTTP:
  2xx: 117043384
  3xx: 0
  4xx: 0
  5xx: 0
Sockets:
  created/s: 54828 (max 55333)
  summary  : 3251998
  errors   : 0
Quantiles:
  0.50: 220.00µs
  0.75: 281.00µs
  0.90: 370.00µs
  0.95: 431.00µs
  0.99: 641.00µs
  1.00: 129.70ms
```

Здесь - `planned` - это планируемая нагрузка по-профилю, а `RPS` - фактическая, которая может быть либо примерно равна планируемой, либо быть меньше, в зависимости от того, как себя чувствуют рилы, сам танк либо L3 балансер.
Например, в конце стрельб они явно отличаются, что свидетельствует о том, что танк не может до конца вывезти указанный профиль нагрузки:
```bash
Requests:
  planned : 4999710
  RPS     : 3280859 (max 3457629)
  summary : 660254593
  timeouts: 0
Transfer:
  tx: 472.393 Mbit/s
  rx: 3.465 Gbit/s
HTTP:
  2xx: 660255746
  3xx: 0
  4xx: 0
  5xx: 0
Sockets:
  created/s: 91197 (max 95839)
  summary  : 18341257
  errors   : 0
Quantiles:
  0.50: 332.00µs
  0.75: 470.00µs
  0.90: 658.00µs
  0.95: 842.00µs
  0.99: 1.30ms
  1.00: 1.47s
```

Число таймаутов и I/O ошибок в идеале должно быть нулевым, но всякое может быть.

### Результаты стрельб
Результаты стрельб можно посмотреть на графиках:
- [Танка](https://grafana.yandex-team.ru/d/ar1ALXxZz/yanet?orgId=1&from=now-5m&to=now&refresh=5s&var-host=vla1-4lb25a-25d&var-interfaceName=All)
- [YaNET@L3](https://grafana.yandex-team.ru/d/mUC6MG0nk/yanet-l3-tank?orgId=1&from=now-5m&to=now&refresh=5s)

## Рилы
К рилам определены следующие требования:
- Обработка **настоящего** HTTP запроса и максимально быстрый ответ.
- Обработка UDP запроса. Ответ не особо интересен, можно просто отсылать назад то, что прилетает в рил.
- Возможность отвечать на балансерные чеки.
- Максимальная производительность.

Последнее требование обусловлено тем, что чтобы нагрузить балансер нагрузкой более чем десять миллионов запросов в секунду - эти запросы должен кто-то обрабатывать.
Иначе очень быстро упремся в количество железа.

Поэтому стандартный для таких случаев nginx не особо подходит - он упирается в примерно 300'000 запросов в секунду.

Вместо этого, в качестве HTTP сервера мы взяли одного из лидеров [techempower](https://www.techempower.com/benchmarks/) бенчмарков - actix-web.
Его примерные пределы производительности - 7'000'000 RPS с включенным HTTP keep-alive. С учетом того, что в стандартном режиме стрельб каждые N запросов происходит пересоздание соединения, то наши замеры показали производительность порядка 4'000'000 RPS на одну машину.

В качестве же UDP "сервера" была написана eBPF программа, которая разворачивает туннеллированный пакет и меняет у него src и dst заголовки на всех уровнях протоколов.
Поскольку в userspace пакет даже не поднимается, то оценить пределы производительности такого рила оказалось проблематично, но точно известно, что одна машина переваривает не менее 10'000'000 UDP пакетов в секунду.

Все это добро может быть установлено через пакет `bang-rs`, который лежит в репозитории `noc`. Он привозит за собой два `systemd` юнита: `bang-http` и `bang-xdpong`.

В итоге, на каждой из 6 машин с рилами развернуто по одному или несколько серверов, в зависимости от конфигурации, и дополнительно в ядро вгружена eBPF.
