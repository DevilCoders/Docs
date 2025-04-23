## Что где живет
  * Прод: https://graphene.yandex-team.ru
  * Тестинг: https://graphene-test.yandex-team.ru
  * Документация: https://wiki.yandex-team.ru/nocdev/graphene
  * Сервис (тестинг): https://deploy.yandex-team.ru/project/graphene-test-stage
  * Сервис (прод): https://deploy.yandex-team.ru/project/graphene-prod-stage
  * Код: arcadia/noc/graphene
  * ABC: http://abc.yandex-team.ru/services/graphene


## Локальный запуск
  1. Создаем файл `config.mk`, содержащий [токен Соломона](https://yav.yandex-team.ru/secret/sec-01dsg2vtknxbsd6364kxd51n47/explore/versions):
```
export SOLOMON_TOKEN = ... - личный oauth токен в solomon
export INVAPI_TOKEN = ... - личный oauth токен в invapi
```

  2. Если в докере не работает IPv6, делаем так:
```
sudo ip6tables -t nat -A POSTROUTING -s fd00::/64 -j MASQUERADE
```

  3. Делаем `make cache`

  4. Делаем в разных терминалах: `make run-nginx`, `make run-graphene` и `make run-grafana`.

  5. Открываем http://localhost:8080

  6. ???

  7. PROFIT!


## Выкладка графаны (графен кеэшер и сервер катятся автоматом через CI, смотри a.yaml)
  1. Убеждаемся, что в репозитории нет незакомиченных/закешированных изменений.

  2. Релизим новую версию. Команда запустит сборку образа и запушит все это дело в реджистри:
```
$ make push-image
```
  3. Идем в деплой: https://deploy.yandex-team.ru/project/graphene-test-stage (тестинг для примера) и катим заменив везде в боксах версию образов.

## graphne как datasource для grafana.yandex-team.ru
Есть 2 варианта, статический и динамический.

### Статические запросы в graphene
Тут просто загружаем дашборд в графене и смотрим на запрос в любой панельке, этот json можно перенести в grafana.

### Динамический запрос в graphene
В этом случае запрос в datasource будет выполнять всю логику обрабоки запроса, как делает графен на запрос дашборда.
Для формироавиня такого запроса в datasource нужно
  1. Взять запрос из графена, например `graph=bytes aux=*solomon* host=vla1-5s108 group_by=host`
  2. Сконвертировать его в `json` пример `{"graph": "bytes", "aux": "*solomon*", "host": "vla1-5s108", "group_by": "host"}` (hint: подсмотреть этот json можно в dev панле браузара, искать запрос в /dashboard)
  3. Добавляем статическую часть в полученный `json`: `"project": "noc", "time_interval": "$timeFilter"`
  4. Полученный json использовать как запрос в datasource графаны.

Пример полного запроса
```json
{
  "graph": "bytes", "aux": "*solomon*", "host": "vla1-5s108", "group_by": "host", 
  "project": "noc", "time_interval": "$timeFilter"
}
```



## Примеры запросов, на которых можно проверить идентичность вывода для тестинга и прода

NOTE: Список дает некоторый базовый набор запросов и не претендует на то, чтобы охватить всю функциональность
```
# криво генерился график NOCDEV-2129
graph=[lasers packets errors] host=myt-s24 iface=100GE1/0/7

# группировка по времени NOCDEV-2276
graph=qos_bytes host=man-e* remote_host=man-32z* time_group_by=10m

# labels NOCDEV-4607
graph=bytes sensor=tx host=neun iface=ae0.0 aux="Eurasia-IX 100GE@M9" labels=%peer%
graph=bytes aux=*.kp.* graph_name=[host iface aux]
graph=bytes aux=*.music.* graph_name=[host iface aux]

# больше максимума метрик (>10к) NOCDEV-3034 - не должен грузиться
graph=errors dc=SAS remote_dc=!SAS top=10

# top по офисному оборудованию NOCDEV-2147
graph=bytes host=longliner top=3

# cloud-ные свичи  NOCDEV-5890
graph=bytes host=myt-0ca3

# cloud roles
graph=bytes role=cloud_cx host=vla-1cx* group_by=iface top=6

# NOCDEV-6662 iface_type 
graph=errors  host=vla1-e*   iface_type=logical  group_by=[class remote_host ]   aux=*FB*

# NOCDEV-1817 pod-view plane-view module-view
graph=[bytes ] remote_type=spine2 iface_type=logical host=man-11d* group_by=plane

# NOCDEV-3832 баг с group_by, в запросе появляются лишние линки
graph=bytes sensor=tx host=/vla-(17|16)x1/ iface=[100GE1/1/11 100GE1/3/11] remote_host=vla-38d1 group_by=plane
graph=bytes sensor=tx host=/vla-.*x1/ iface=100GE1/*/11 remote_host=vla-38d1 group_by=[remote_host]
graph=bytes host=[man1-x1 man1-x2] remote_type=spine1 remote_host=man-1d2   iface=100GE* sensor=rx group_by=remote_host
# trfc from vla-32ds to vla-32z by class
graph=[qos_bytes    ] host=vla-32d* remote_host=vla-32z*   group_by=[class remote_host ] class=[0 1 3]
# group_by class with remote_host in query
graph=[qos_bytes] host=[vla-32d1 vla-32d2] iface_type=phy remote_host=vla-32z* class=0 group_by=class sum_by=iface

# cols
graph=qos_bytes host=man-e* remote_host=man-32z* time_group_by=10m cols=6

# top
graph=[bytes packets  errors] host=/man-32z*/ iface=[/ae1\d$/] top=3
# top with nodata
graph=bytes host=sas1-1fw10  iface=vlan* top=2

# NOCDEV-6701 via grafana's overrides and transformations
graph=bytes_percent  host=neun iface=ae0.0 aux="Eurasia-IX 100GE@M9" labels=%peer%
graph=[bytes_percent  packets errors] host=sas-32z1 iface=et-0/0/5
graph=[bytes_percent  packets  errors_percent] host=/man-32z*/ iface=[/ae1\d$/] top=3

# NOCDEV-6550 - переопределение сенсоров графика
graph=[bytes errors] host=/man-32z[7-9]/ iface_type=logical group_by=host sensor=rx

# all others
#
graph=[bytes errors] host=/man-32z[7-9]/ iface=[/ae1\d$/] group_by=host
graph=bytes host=/sas-\d\dd\d/ remote_type=spine2 group_by=host iface=[Eth-Trunk* ae* po*] sensor=tx
graph=device-buffers host=/sas.*-\d+s\d+/ sensor=used group_by=host top=10
graph=bytes host=sas-32d* remote_type=spine2 sensor=rx group_by=host iface=[100GE* Ethernet* et-*]
graph=bytes dc=Сасово type=spine2 group_by=host remote_type=spine1 sensor=rx
# trfc from vla-z to vla-e
graph=[packets bytes   ] host=vla-32z* remote_host=vla1-e*  iface=Eth-Trunk* group_by=remote_host sensor=tx sum_by=host
# trfc from vla-z to vla-e by class
graph=[qos_bytes    ] host=vla-32z* remote_host=vla1-e*  iface=Eth-Trunk* group_by=[class remote_host ] class=[0 1 3] sum_by=host
# trfc from vla-e to FB-p
graph=[ bytes   ] host=vla1-e*   iface=[Eth-Trunk* ae*] group_by=[class remote_host ] class=[0 1 3]  aux=*FB* sensor=tx
# same but drops
graph=errors  host=vla1-e*   iface=[Eth-Trunk* ae*] group_by=[class remote_host ]   aux=*FB*

# drops at vla-32z* to vla1-e* by class 8 (sum of all classes)
graph=qos_drops  host=vla-32z* remote_host=vla1-e*  iface=Eth-Trunk* group_by=remote_host  sensor=queue_discarded_packets class=8
# vla D to X
graph=[bytes ] host=/vla-4\dd\d/ remote_host=/vla-[1-8]x.*/ group_by=host sensor=tx
# vla D from TOR
graph=[bytes ] host=/vla-40d1/ remote_host=/vla2-.*s.*/  sensor=rx
# per queue
graph=qos_bytes host=[std-p1 m9-p2 sp1-m9] remote_host=man-e* group_by=class aux=/.*FB.*/ sum_by=[host iface]
# FB per queue
graph=qos_bytes host=[vla1-e*] remote_host=[sas-e* m9-p2 std-p1] aux=/.*FB.*/ sum_by=remote_host class=2
# MAN errors RX MAN
graph=errors remote_host=[m9-p* std-p*] host=[man-e* jansson sibelius aurora pallada] iface=[100GE* et-*] graph_name=[host iface aux] sensor=rx_errs group_by=host
# RX RUS
graph=errors host=[m9-p* std-p*] remote_host=[man-e* jansson sibelius aurora pallada] iface=[100GE* et-*] graph_name=[host iface aux] sensor=rx_errs group_by=host

```
