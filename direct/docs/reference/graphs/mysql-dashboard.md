# MySQL Дашборд
Параметризованный дашборд про кластера наших баз в MDB. Ссылки (*открывайте в новом окне*):
<iframe height='120' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=direct&cluster=mdb_mdbmj3sd1jng6ga2d4lv&l.instance=ppcdata16&dashboard=mdb-mysql-links&graphOnly=y'></iframe>
Переключиться на нужную базу можно по ссылкам из правого блока на самом дашборде



## Что есть
Те графики, что для мастера или реплик — в каждый момент времени показывают данные соответствующего хоста.
Т.е. если было переключение мастера за период наблюдений — то линия на графике будет означать две разные машины.

### Connections
График числа подключений к каждому из хостов кластера.
Также указаны пороги для алерта на число подключений.

### Running threads
График активных тредов на всех хостах кластера.
Показывает "занятость" MySQL обработкой запросов. Рост может свидетельствовать о медленных запросах или повышении внешней нагрузки.

### Is Alive / Is Primary
Показывают живость хостов кластера во времени, и кто является мастером.

### CPU primary
Утилизация CPU на _мастере_, в ядрах:
- Userspace — утилизация MySQLем
- System - потребление системой
- Guarantee / Limit — гарантия на CPU и ограничение контейнера
- Wait — троттлинг контейнера (когда внутри дана нагрузку выше Limit)

### Replication lag
Отставание репликации, в секундах. Замеряется силами MDB (?), не по таблице heartbeat Директа.

### Queries / Slow Queries
По всем хостам в кластере: общее число запросов и тормозные запросы.

### Network bytes
Два графика: primary — на мастере, replica — на репликах.

RX — прием, TX — передача.
Кроме этого отмечены лимит и гарантия контейнера по пропускной полосе.

### Free space
График свободного места по хостам на разделе с MySQL и пороги, по которым реплика уйдет в RO.

### Disk IO, primary
Дисковая утилизация на мастере. Чтение, запись и лимт со стороны контейнера.

### Juggler
Некоторые juggler-проверки про этот кластер БД. Собраны по тегу.

## пример в iframe
<iframe height='1400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=direct&dashboard=mdb-mysql&cluster=mdb_mdbmj3sd1jng6ga2d4lv&instance=ppcdata16&b=6h&e=&graphOnly=&graphOnly=y'></iframe>

## источник
Дашборд сгенерирован с использованием [solo](../../glossary/glossary.md#solo).
Описание лежит в [аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/dashboard/mysql.py).
