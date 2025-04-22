Сервис для сканирования доступности большого числа хостов. Использует zmap под капотом.

Схема сервиса:\
[<img src="https://jing.yandex-team.ru/files/gescheit/megaping2.jpg" width="1000"/>](https://jing.yandex-team.ru/files/gescheit/gfglister.jpg)

Конфигурация:

```yaml
db: # опции из psycopg2.connect
# дефолтные
# host = "vla-9unjkch6y49bpo1t.db.yandex.net,man-3ffnv8kvj78g7cqd.db.yandex.net"
# port = 6432
# dbname = megaping
# user = megaping
# connect_timeout = 10
# target_session_attrs определяет по типу instance
  host: "host1,host2,host3"
  password_file: /etc/megaping_db_password # пароль из файла
  password: ololo # или просто пароль

instances:
  discovery_icmp: # просто имя
    zmap_type: discovery # сканер новых доступных адресов
    check_type: icmp # еще есть tcp_80
    interval: 3600
    setpoint: 1000  # ожидаемое количество хостов в одной AS
    rate: 100000 # максимальный rps - https://nda.ya.ru/t/qNsi-w0n5GKHBi
  check_icmp:
    zmap_type: check_recalc # проверка насканированных адресов и удаление недоступных
    smart_decrease: true
    check_type: icmp
    interval: 50
    rate: 10000
  check_icmp2: # просто проверка доступности
    check_type: icmp
    interval: 120
    namespace: megaping
    zmap_type: check
solomon:
  auth_type: OAUTH # OAUTH or IAM
  token: OLOLO # for OAUTH
  url: http://solomon.yandex.net/api/v2/push
```

Как это работает:\
Discovery instance проверяет количество доступных адресов в таблице Targets и если их недостаточно,
то запускается поиск новых адресов. Префиксы берутся из таблицы FullView, а результат сохраняется в Targets.
Instance check с опцией smart_decrease проверяет доступность и удаляет адреса, если долго не отвечают.
Простой instance check проверяет доступность адресов и отправляет результат в solomon.

Метрики:

Сервис **duration**.\
Длительность выполнения функций.

Сервис **data**.\
Результат проверки доступности. Сенсор **decrease** - количество недоступных хостов в выбранном origin (AS),
**increase** - доступных, **megaping** отнормированная метрика доступности origin, учитывающая вес origin и количество доступных адресов.
**process_ips** - количество проверенных адресов. **rtt** - средний rtt.

Зависимости:
```shell
apt-get install zmap
```
Версия должна быть что-то вроде 2.1.2-noc1. Стандартная убунтовская не содержит необходимых патчей.
