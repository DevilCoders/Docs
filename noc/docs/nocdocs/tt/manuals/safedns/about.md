Введение
========
[оригинал доки тут](https://wiki.yandex-team.ru/traffic/safedns/)

Сервис Яндекс.DNS представляет из себя публичный рекурсивный DNS резолвер в трёх вариациях: 
 * стандартный (common) - не модифицирует DNS ответы
 * безопасный (safe) - подменяет ответы на запросы о доменных именах из списка "угрозы" на CNAME [safe1.yandex.ru](https://racktables.yandex-team.ru/index.php?page=ipvs&tab=default&vs_id=629)
 * семейный (family) - дополнительно к тому что делает safe, также подменяет ответы на запросы о доменных именах из списка "порно" на CNAME [safe2.yandex.ru](https://racktables.yandex-team.ru/index.php?page=ipvs&tab=default&vs_id=331), подменяет запросы к доменным именам "поиск Яндекс" на [familysearch.yandex.ru](https://racktables.yandex-team.ru/index.php?page=ipvs&tab=default&vs_id=228), подменяет запросы к доменным именам "поиск Google" на forcesafesearch.google.com

Технически резолвер реализован в виде группировки контейнеров (stage [safedns-prod](https://deploy.yandex-team.ru/stages/safedns-prod/status/)) в системе Yandex Deploy, развернутых в трёх ДЦ: SAS, VLA и MAN. Помимо резолвера каждый контейнер реализует:
 * поставку логов DNS запросов и ответов в таблицу YT через Logbroker
 * отгрузку ответов авторитетных серверов в SIE (Farsight Security), а также партнёрам: Kaspersky и RiskIQ
 * отгрузку логов и метрик самого контейнера в Logbroker и Solomon, соответственно

Логи DNS в YT таблицах необходимы для а) разбора обращений пользователей и б) отгрузки части данных из этих логов в VirusTotal, который взамен предоставляет некоторое количество запросов в свой сервис.
Ответы авторитетов в SIE отгружаются взамен доступа к информации в нём же. Партнёры (Kaspersky, RiskIQ) получают эту инормацию **TBD**.

Быстроссылки
============

 * [Stage в Yandex Deploy](https://deploy.yandex-team.ru/stages/safedns-prod/status)
 * [Дашборд в Grafana](https://grafana.yandex-team.ru/d/eTQJnQZnk/safe-dns?orgId=1&refresh=30s)
 * [Namespace в Juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Dsafedns)
 * [Cluster в Solomon](https://solomon.yandex-team.ru/admin/projects/tt/clusters/tt_safedns)
 * Таблицы [threats](https://yt.yandex-team.ru/arnold/navigation?path=//home/antivir/prod/export/dns/threats) и [porno](https://yt.yandex-team.ru/arnold/navigation?path=//home/antispam/export/dns/porno) в YT
 * Сервисы [dns.yandex.ru](https://l3.tt.yandex-team.ru/service/14116), [safe.dns.yandex.ru](https://l3.tt.yandex-team.ru/service/14117) и [family.yandex.ru](https://l3.tt.yandex-team.ru/service/14119) в L3 Manager
 * [Планировщик в Sandbox](https://sandbox.yandex-team.ru/scheduler/196718/tasks?hidden=true&all_tags=false&all_hints=false&limit=20)
 * [Релизное правило в Yandex Deploy](https://deploy.yandex-team.ru/stages/safedns-prod/release_rules/safedns-prod-rule)
 * [Исходники в Arcadia](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns)
 * Конфиги Logfeller: [парсер](https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/traffic-safedns-log.json), [логи](https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/traffic_hume_logs.json) и [стримы](https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/traffic_hume_streams.json) (**на данный момент смотрят в тестовый топик Logbroker и тестовый кластер YT**)

Движущиеся части
================

Резолвер
--------

Реализован тремя пареллельно запущенными процессами unbound, каждый из которых имеет разную конфигурацию, удовлетворяющую требованиям к common, safe или family варианту. Каждый из них слушает соответствующий набор адресов и выделенный порт на localhost. Порт на localhost используется для работы [liveness probe](https://deploy.yandex-team.ru/docs/concepts/pod/workload/probes#liveness-proba) Y.Deploy. Резолверы поддерживают управление через [unbound-control](https://www.nlnetlabs.nl/documentation/unbound/unbound-control/), а также выгружают логи запросов и ответов в UNIX socket с помощью механизма [dnstap](http://dnstap.info/). dnstap выгружает внутренние структуры процесса в виде protobuf, таким образом предоставляя эффективное логирование всех запросов и ответов.
Подмена ответов в safe и family вариантах реализована через RPZ (response policy zone), которые представляют собой специальные файлы зон, определяющие действие при получении запроса на доменное имя из такой зоны. В нашем случае резолверы отдают определенный CNAME, который приведет пользователя на заглушку (HTTP) или сломает подключение (HTTPS). Зоны обновляются связкой Sandbox задачи [SAFE\_DNS\_CONFIG](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/traffic/safe_dns_config/__init__.py) и релизного правила [safedns-prod-rule](https://deploy.yandex-team.ru/stages/safedns-prod/release_rules/safedns-prod-rule) в Yandex Deploy. Сами наборы доменных имен поддерживаются в YT таблицах командами Antimalware: [threats](https://yt.yandex-team.ru/arnold/navigation?path=//home/antivir/prod/export/dns/threats) и [porno](https://yt.yandex-team.ru/arnold/navigation?path=//home/antispam/export/dns/porno).

dnstap-коллектор
----------------

Выгрузка логов запросов и ответов из процессов unbound отправляется в UNIX socket, на другом конце которого слушает dnstap-коллектор - [golang-dnstap](https://github.com/dnstap/golang-dnstap). Коллектор сам создаёт socket при запуске, а принимая логи конвертирует их в JSON и сохраняет в файл. При получении SIGHUP коллектор переоткрывает файл лога, обеспечивая возможность ротации. Эта реализация коллектора выбрана потому что а) умеет конвертировать protobuf в JSON и б) Golang позволяет собрать один исполняемый файл со всеми зависимостями.

push-client
-----------

Общеяндексовое приложение для поставки логов в Logbroker [push-client](https://wiki.yandex-team.ru/logbroker/docs/push-client/). Применяется для доставки логов DNS (dnstap) в Logbroker. Лог вычитывает из файла, откладываемого dnstap-коллектором. Выбран вместо unified-agent, потому как последний требует отправку логов прям в него силами приложения. Это значит что нужно либо написать приложение-прослойку, либо форкать внешнее приложение (golang-dnstap) и править. При этом клиентской библиотеки для Golang [нет](https://st.yandex-team.ru/UNIFIEDAGENT-151). Поэтому push-client.

sie-dns-sensor
--------------

[sie-dns-sensor](https://www.farsightsecurity.com/technical/passive-dns/passive-dns-sensor/) - урезанный вариант [nmsgtool](https://github.com/farsightsec/nmsg), специально для сбора и отправки DNS данных. С помощью libpcap слушает на указанном в конфигурации интерфейсе собирая ответы авторитетных DNS серверов локальному резолверу. Полученные пакеты агрегируются, пакуются в файлы с расширением nmsg и отправляются в SIE/Farsight через rsync/SSH. Для отправки использутся [private key](https://yav.yandex-team.ru/secret/sec-01fa3fyvp0tv966kn7d33dbcwx/explore/versions), скопированный во все контейнеры.
В виду особенностей нашей ДЦ фабрики, а именно туннелирования IPv4, мы имеем два разных интерфейса, используемых для общения с Интернет. Конфигурация SIE позволяет указать только один интерфейс, приходится выбирать. Пока выбираем туннель и IPv4.

sie-sender
----------

[bash скрипт](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/misc/sie-sender), который делает hard link'и nmsg файлов в отдельные директории и с помощью rsync/SSH отправляет эти файлы в Kaspersky и RiskIQ. Для отправки используется тот же private key, что и в SIE.

dnsl3r
------

Вспомогательная [утилита собственного изготовления](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/dnsl3r). Представляет из себя web-сервер (python/sanic), который отвечеает на health check'и балансировщиков/keepalived. Используется HTTP\_CHECK. Это необходимо потому как балансировщик не может надежно проверить готовность DNS резолвера принимать нагрузку. Как правило в этом случае используется TCP\_CHECK на порт 53, но он не говорит о готовности резолвера. В нашем случае запуск family инстанса unbound происходит очень быстро и он сразу готов принимать TCP соединения, но обрабатывать запросы он не может в течении ~7 минут, пока не прочитает все RPZ. Это грозит проливом трафика.
dnsl3r сам опращивает резолверы с помощью библиотеки asyncdns и в случае готовности ответчает на запросы балансера кодом 200.

puma
----

Ещё одна вспомогательная [утилита собственного изготовления](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/puma). Получает метрики резолверов с помощью unbound-control, высчитывает их rate и отправляет в Solomon. Push модель не позволяет использовать тип метрик RATE, поэтому приходится считать самому. С другой стороны pull модель, предполагающая использование solomon-agent для сбора интересующих данных предлагает лишь вызов скриптов на Python 2, что не особо актуально в 2021. Для получения метрик из unbound-control используется команда `stats_noreset`. Вообще весь механиз сбора и отправки метрик был нагло скопирован из [d2](https://a.yandex-team.ru/arc/trunk/arcadia/noc/traffic/dns/junk/d2), спасибо slayer!

sysmond
-------

Общеяндексовая [утилита](https://docs.yandex-team.ru/solomon/data-collection/sysmond/overview) сбора и отправки системных метрик (CPU, memory, disk, etc...). Работает в pull модели.

Релизы
======

Обновление файлов RPZ реализовано через [релизную интеграцию](https://deploy.yandex-team.ru/docs/concepts/release-integration/release-integration). В Sandbox запущен [планировщик](https://sandbox.yandex-team.ru/scheduler/196718/tasks?hidden=true&all_tags=false&all_hints=false&limit=20), который раз в N часов (предплоагается что N = 1) запускает задачу типа SAFE\_DNS\_CONFIG. Задача преобразует содержимое YT таблиц со списками доменных имён в файлы RPZ, после чего создает релизный тикет. В Deploy создано релизное правило, согасно которому такие тикеты автоматически выполняются, пересобирая контейнеры с новыми RPZ. Пересбор контейнеров ведет к их выключению и повторному запуску. Задачу можно было решить через динамические ресурсы, но необходимость перезапускать резолверы и ждать пока они вычитают RPZ от этого бы не исчезла. Так пусть Deploy делает всё сам.
Предполагается что надобность в этом механизме отпадёт, когда списки доменов будут загружаться в YP (NEED LINK!!!).

Stop policy
===========

Контейнер может быть перезапущен в результате релиза или миграции. Релизы как описано выше происходят регулярно и автоматически. YP, который является планировщиком ресурсов в Yandex Deploy, не даёт гарантий что контейнер будет всегда привязан к одному хосту. И конечно возможны неисправности. Для того чтобы плавно выключать контейнер, не проливать трафик и не терять логи используется [stop policy](https://deploy.yandex-team.ru/docs/concepts/pod/workload/probes#stop-policy). В нашем случае оно достаточно простое и для всех workload, кроме dnsl3r, выглядит как `sleep 180`. Для dnsl3r - `touch /var/run/dnsl3r_stop & sleep 180`. Это позволяет сигнализировать балансировщикам об отключении, после чего закончить дела: поставить логи и метрики, отправить данные в SIE и партнерам.

Мониторинги и метрики
=====================

Мониторинг выполнен комбинацией Solomon и Juggler. Метрики контейнера Solomon **pull**ит из sysmond, запущенного в качестве workload. Метрики unbound'ов **push**ит puma. Все эти метрики попадают в [кластер safedns](https://solomon.yandex-team.ru/?project=tt&cluster=safedns), на них настроено некоторое количество алёртов в [admin](https://solomon.yandex-team.ru/admin/projects/tt/alerts) (смотреть те что начинаются с safedns). Результаты этих проверок уходят в Juggler в виде сырых событий.
Также в контейнреах развёрнут [Juggler subagent](https://deploy.yandex-team.ru/docs/how-to/monitorings/settings#juggler), который запускает некоторое количество пассивных проверок, собранных в [бандл](https://docs.yandex-team.ru/juggler/client/bundles#how-to-build), а также принимает пуши событий отправки данных в SIE/RiskIQ/Kaspersky.
Есть дашборд в [Grafana](https://grafana.yandex-team.ru/d/eTQJnQZnk/safe-dns?orgId=1&refresh=30s).
Namespace в Juggler - [safedns](https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Dsafedns)
Что проверяется сейчас:
 * sie\_send - nmsg файлы SIE успешно отправляются в Farsight, RiskIQ и Kaspersky. Скрипты, отправляющие эти данные пушат события в Juggler subagent через скрипт push\_to\_juggler.
 * push-cleint-status - набор проверок push-client, написанный командой Logbroker, собираются в наш бандл и запускаются как пассивные проверки.
 * rpz\_freshness - [скрипт](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/juggler/checks/fresh_rpz.py), запускается как пассивная проверка (часть нашего бандла) и проверяет ctime RPZ, он должен быть свеж из-за регулярных релизов
 * rpz\_creation - Sandbox задача SAFE\_DNS\_CONFIG пушит результат своей работы в [глобальную ручку](https://docs.yandex-team.ru/juggler/raw_events#global-push). Мониторим её, так как от неё зависит процесс релизов.
 * num\_servfail - кол-во SERVFAIL результатов, если их много - у нас какая-то проблема с резолвом; Solomon алёрт.
 * timings\_errs - CDN сервера периодически опрашивают резолверы, результаты этих опросов сливают в Solomon (заведует этим slayer), проверяем что времена ответов не превышают некоторый порог; Solomon алёрт.
 * loadavg - load average CPU контейнеров; Solomon алёрт.
 * num\_queries\_total - кол-во RPS, проверяем что контейнеры не перегружены; Solomon алёрт.
 * l3\_svc\_\*\_dns\_yandex\_ru - состояние анонсов и RS L3-сервисов; алёрты [slbcloghandler](https://clubs.at.yandex-team.ru/noc/3588)
Juggler бандл собираем задачей [BUILD\_JUGGLER\_CHECKS\_BUNDLE](https://sandbox.yandex-team.ru/task/1059163049/view), отдавая её [bundle.json](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/juggler/bundle.json).

Порт 1253
=========

По договоренности с Zyxel резолверы слушают ещё и на порту 1253 (https://st.yandex-team.ru/CACHEDNS-100). Похоже необходимость в этом давно отпала, но какой-то трафик по старинке туда идёт.

Содержимое контейнера
=====================

Контейнер представляет из себя один [box](https://deploy.yandex-team.ru/docs/concepts/pod/box), на который накладывается множество [слоев](https://deploy.yandex-team.ru/docs/concepts/pod/podagentpayload/resources/layer), добавляется небольшое количество [статических ресурсов](https://deploy.yandex-team.ru/docs/concepts/pod/podagentpayload/resources/staticresource) и запускается некоторое количество [workloads](https://deploy.yandex-team.ru/docs/concepts/pod/workload/workload).
Box - это мета-контейнер, под которым запускаются процессы, и volume. Слои накладываются OverlayFS, если вы впервые видите эту концепцию можно представить её как склеивание двух слепков файловой системы, где верхний слепок "перекроет" то что было в нижнем при совпадении. Статические ресурсы - это директории смонтированные в контейнер, в первую очередь используются для секретов, которые необходимо записать в файл. Workload - это процесс запускаемый в box.

#|
|| **название**       | **тип** | **описание**       | **метод доставки** ||
|| default image | layer | Базовый слой, предоставляемый Y.Deploy. Используется [bionic app](https://wiki.yandex-team.ru/runtime-cloud/virtualimages/#minimalnyjjobraz). Выбран как самый свежий (focal не предлагают) и минимальный по объёму. | предоставляется самим Y.Deploy ||

|| safedns\_porto | layer | Слой, созданный через Sandbox задачу [BUILD\_PORTO\_LAYER](https://sandbox.yandex-team.ru/task/1017625610/view). Задача берёт базовый образ, монтирует его в систему и выполняет [скрипт](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/misc/create_porto_layer). Исользуется для того чтобы установить в образ sie-dns-sensor. Иначе принести приложение на C, требуещее определенное количество зависимостей - невозможно. | Sandbox задача BUILD\_PORTO\_LAYER ||
|| unbound | layer | Исполняемый файлы unbound и сопутствующих утилит. Основной элемент нашего сервиса. Релизы новых версий происходят в UNBOUNDREL-2. | Sandbox задача [YA\_PACKAGE](https://sandbox.yandex-team.ru/resource/2231328487/view). ||
|| [unbound\_conf\_template](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/misc/unbound_config_template) | layer | Шаблон конфигурации unbound. Используется, так как нам нужно запустить три резолвера с почти идентичной конфигурацией. | ya upload ||
|| named.root | layer | root-hints файл, используемый unbound для определения корневых DNS серверов. | регулярная Sandbox задача SAFE\_DNS\_CONFIG ||
|| threats.rpz | layer | RPZ с доменными именами, распространяющими вирусы/трояны/malware, занимающиеся фишингом и т.д. Применяется в safe и family резолверах. | регулярная Sandbox задача SAFE\_DNS\_CONFIG ||
|| porno.rpz | layer | RPZ с доменными именами, распространяющими порнографические материалы. Применяется в family резолвере. Доставляется как часть релиза зон. | регулярная Sandbox задача SAFE\_DNS\_CONFIG ||
|| gsearch.rpz | layer | RPZ с доменными именами страниц Google поиска на разных языках. Применяется в family резолвере для переадресации на безопасный поиск Google. | регулярная Sandbox задача SAFE\_DNS\_CONFIG ||
|| yasearch.rpz | layer | RPZ с доменными именами страниц Yandex поиска на разных языках. Применяется в family резолвере для переадресации на безопасный поиск Yandex. | регулярная Sandbox задача SAFE\_DNS\_CONFIG ||
|| dnstap | layer | golang-dnstap - приёмник логов в формате dnstap. | ya upload ||
|| pclient\_binary | layer | Исполняемый файл push-client. Получен перепаковкой Sandbox релиза. Заходим в [Sandbox](https://sandbox.yandex-team.ru/resources?type=STATBOX_PUSHCLIENT&limit=20&created=6_months) и на вкладке ресурсы ищем за последние полгода ресурсы типа STATBOX\_PUSHCLIENT. Перепаковка потребовалась потому что оригинал не архивирован, а Deploy пытается его распаковать. Поэтому скачали - запаковали - доставили через ya upload. | ya upload ||
|| [pclient\_configuration](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/misc/push_client.yaml) | layer | Конфигурационный файл push-client. | ya upload ||
|| dnsl3r\_binary | layer | dnsl3r - web-приложение которое отвечает на проверки keeaplived/L3LB. | ya upload ||
|| [logrotate\_layer](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/misc/rotate_it) | layer | Конфигурационный файл logrotate в директории etc/logrotate.d/. logrotate в контейнерах Deploy есть по-умолчанию, нужна только конфигурация. | ya upload (должен быть помещен в /etc/logrotate.d/) ||
|| solomon\_sysmond | layer | sysmond - приложение которое собирает системные метрики, которые PULL'ит Solomon. Ресурс скопирован из dns-cache, похоже был создан через ya upload. | ya upload ||
|| puma | layer | puma - приложение, собирающие метрики резолверов, используя unbound-control. Метрики PUSH'атся в Solomon. | ya upload ||
|| [sie\_launcher](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/misc/sie-launcher) | layer | Bash скрипт, запускающий sie-dns-sensor. | ya upload ||
|| [sie\_config\_template](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/misc/sie_config_template) | layer | Конфигурационный файл (на самом деле скрипт, который только определяет переменные) для sie-dns-sensor. | ya upload ||
|| [sie\_sender](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/misc/sie-sender) | layer | Скрипт, в цикле отправляющией nmsg файлы в RiskIQ и Kaspersky | ya upload ||
|| [push\_to\_juggler](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/push_to_juggler) | layer | Python-скрипт который пушит резултьтаты отправки данных в партнеров в Juggler (локальный агент или глобальную ручку) | ya upload ||
|| [init\_script](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/misc/init_box) | layer | Bash скрипт, выполняющий подготовку box к работе. Совершает следующие действия: настраивает туннели и IP правила, для обработки трафика от балансировщиков; создаёт необходимые директории и настраивает права доступа к ним; создаёт конфигурацию SIE из шаблона; создаёт конфигурации резолверов из шаблона; добавляет символьные ссылки на исполняемые файлы. | ya upload ||
|| [unbound\_secrets](https://yav.yandex-team.ru/secret/sec-01f9ksfv0174pdtdabc1qm6h77/explore/versions) | static resrouce | Создаёт 5 файлов, наполняя их секретами. 4 файла обеспечивают authentication между unbound-control и резолверами, см. [man unbound.conf](https://nlnetlabs.nl/documentation/unbound/unbound.conf/), раздел "Remote Control Options".  Пятый файл содержит DNSKEY запись корневых серверов, используется как trust-anchor-file в конфигурации unbound. | secret delegation ||
|| [sie\_key](https://yav.yandex-team.ru/secret/sec-01fa3fyvp0tv966kn7d33dbcwx/explore/versions) | static resrouce | Создаёт 1 файл, с private ключом, необходимым для загрузки SIE данных по SSH партнёрам. | secret delegation ||
|| [juggler bundle](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/safedns/juggler) | juggler bundle | MANIFEST файл и набор пассивных проверок для Juggler | Sandbox задача BUILD\_JUGGLER\_CHECKS\_BUNDLE ||
|#

Здесь доставка через ya upload означает, что локальный файл (на вашем ноутбуке, сервере и т.д.) превращается в Sandbox ресурс командой

`./ya upload --ttl=inf --type=OTHER_RESOURCE --description='put your description here' $PATH_TO_FILE`

ttl управляет временем жизни ресурса, inf - не ограничена. Если ресурс будет вычищен по TTL, а stage его все ещё использует, пересборка контейнеров сломается. type - тип ресурса, он должен быть известен Sandbox'у, OTHER\_RESOURCE для этого отлично подходит. Утилита ya лежит в корне Arcadia, или же её можно [установить отдельно](https://wiki.yandex-team.ru/yatool/).

[secret delegation](https://deploy.yandex-team.ru/docs/how-to/secrets#kak-zadat-sekrety-v-ui) обеспечена самим Deploy.

Workloads
---------

#|
|| common | unbound резолвер типа common. Не имеет RPZ в конфигурации. ||
|| safe | unbound резолвер типа safe. Имеет RPZ threats в конфигурации. ||
|| family | unbound резолвер типа family. Имеет RPZ threats, porno, gsearch и yasearch в конфигурации. ||
|| dnsl3r | Запущенный DNSL3R - опрашивает резолверы и отвечает на проверки балансировщиков. ||
|| dnstap | Запущенный golang-dnstap. Принимает логи резолверов в формате dnstap через UNIX socket и складывает в файл в виде JSON. ||
|| pclient | Запущенный push-client. Читает JSON из файла, созданного golang-dnstap и отправляет их в Logbroker. ||
|| puma | Запущенная puma. Оправшивает резолверы через unbound-control и отправляет полученные метрики в Solomon. ||
|| sysmond | Запущенный sysmond. Собирает системные метрики (CPU, memory, disk). ||
|| sie | nmsgtool, который запущен посредством sie-launcher. ||
|| sie-sender | Скрипт отправляющий nmsg файлы в RiskIQ и Kaspersky ||
|#

Примеры
=======

Выкладка нового кода/обновление ресурса
---------------------------------------

Для примера возьмём релиз новой версии dnsl3r. После того как мы замержили необходимые изменения в Arcadia - собираем бинарь. Здесь и далее работаем из корня примонтированной Arcadia.
```bash
./ya make traffic/safedns/dnsl3r
# Находим собранный бинарь, в директории указанной при сборке лежит symlink, и копируем в какое-нибудь более удобное место
ls -la traffic/safedns/dnsl3r/bin/
cp /home/darkyman/.ya/build/symres/60114d162f6f9515ee6a219cb646335a/dnsl3r ~/tmp/
# Пакуем в tgz
tar -C ~/tmp -czf dnsl3r.tgz dnsl3r
# И загружаем в Sandbox
./ya upload --ttl=inf --type=OTHER_RESOURCE --description='dnsl3r, version 1.1' ~/tmp/dnsl3r.tgz
# В результате получим ссылку на ресурс в Sandbox, откроем её чтобы найти resource ID и MD5 checksum.
# Получаем текущую конфигурацию нашего stage
./ya tool dctl get stage safedns-prod > ~/tmp/prod-stage
# В файле `~/tmp/prod-stage` находим секцию со слоем dnsl3r, такую:
# - checksum: MD5:6a34ccb4e5166c8604ef128ac798f297
#   id: dnsl3r_binary
#   url: sbr:2387324877   
# В `url: sbr:` подставляем новый resource ID, а в `checksum: MD5:` чек-сумму, сохраняем результат.
# Заливаем обновлённый файл stage.
./ya tool dctl put stage ~/tmp/prod-stage
```
На странице [stage](https://deploy.yandex-team.ru/stages/safedns-prod/status/) можно наблюдать за процессом деплоя.

Как собрать golang-dnstap
-------------------------

У нас есть два "внешних" приложения: sie-dns-sensor и golang-dnstap. Первый написан на C и посему устанавливается deb пакетом в отдельный слой. Второй же написан на Go, что позволяет нам собрать его в один исполняемый файл со всеми зависимостями и принести в контейнер как ресурс. Если вы знакомы с Go, то знаете как это сделать. Я нет. Вот инструкция для таких как я. По сути списана с [блога DO](https://www.digitalocean.com/community/tutorials/how-to-install-go-and-set-up-a-local-programming-environment-on-ubuntu-18-04). Пояснений зачем всё это здесь не будет, только шаги как повторить.

Скачиваем свежий Go и распаковываем в систему
```bash
curl -O https://dl.google.com/go/go1.17.linux-amd64.tar.gz
sudo tar -xvf go1.17.linux-amd64.tar.gz -C /usr/local/
sudo chown -R root:root /usr/local/go
# В домашней директории создаём всякие директории для Go и объявляем их в переменных окружения
mkdir -p $HOME/go/{bin,src}
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin:/usr/local/go/bin
# Проверяем что go работает
go version
# Скачиваем golang-dnstap
go get github.com/dnstap/golang-dnstap
# Собираем исполняемый файл
cd go/pkg/mod/github.com/dnstap/golang-dnstap\@v0.4.0/dnstap
sudo go build
# Проверяем результат
./dnstap --help
# Упаковываем и отправляем в Sandbox
tar -czf dnstap.tgz dnstap
mv dnstap.tgz ~/tmp/
cd ~/arc/arcadia
./ya upload --ttl=inf --type=OTHER_RESOURCE --description='golang-dnstap bindary' ~/tmp/dnstap.tgz
```

Схема
=====
![схема safedns](https://jing.yandex-team.ru/files/dukeartem/safedns.svg "схема safedns" =100%x100%)
[исходник диаграммы](https://nda.ya.ru/t/LcTpHBbH5AC9EJ)


Видео рассказ
=============

https://jing.yandex-team.ru/files/darkyman/zoom_0.mp4

