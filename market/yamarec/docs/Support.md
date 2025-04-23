# Поддержка

- [В начале дежурства](#В-начале-дежурства)
- [Если написали в хотлайн](#Если-написали-в-хотлайн)
- [Если загорелась лампочка](#Если-загорелась-лампочка)

## В начале дежурства

1. Открой [хотлайн](https://t.me/joinchat/CAt9W0EA9cmQisyfId6GvA) и запинь сообщение

   > На этой неделе дежурит @yournickname


## Если написали в хотлайн

Ответь, чо.

Если есть сомнения, то можно либо призвать кого-то конкретного прямо в хотлайн, а можно направить вопрос во внутренний чат.

## Если загорелась лампочка

Уведомления шлет JugglerSearchBot в наш [факап-чат](https://t.me/joinchat/BbgvTERXHp-_ugLrIpafKg).

Если пришел `WARN`, то нужно в течение дня глянуть соответствующие графики/логи.
Замеченные проблемы стоит обсудить в факап-чате.

Если пришел `CRIT`, то нужно оперативно разобраться, временная ли это проблема и найти причину:
- если чинить не нам, то нужно поставить тикет на ответственных с тэгом yamarec-outsource
- если чинить нам, то нужно поставить тикет в MARKETRECOM с тэгом support и приоритетом Critical

О найденной критической проблеме нужно отписаться в факап-чате.

#### yandex_yamarec1_status

> Упал демон сервиса `yandex-yamarec1`.

Зайти на продовые тачки и проверить активность сервиса через `service yandex-yamarec1 status`.
Если он действительно лежит, то изучать `/var/log/yandex/yandex-yamarec1/info.log` на предмет ошибок.

#### yandex_yamarec1_app_health

> Проблемы с веб-приложением, не пингуется.

Проверить ручку `/ping` руками.
Если недоступна, то зайти на продовые тачки и проверить активность сервиса через `service yandex-yamarec-app status`.
Если лежит, то стоит поизучать логи и состояние nginx.
Возможно, потребуется рестарт.

#### yandex_yamarec1_health

> Что-то не так с воркфлоу в проде.

Открываем `/var/log/yandex/yandex-yamarec1/critical.log` на любой продовой тачке и смотрим свежую сводку.
Задачи могут:
- долго выполняться - нужно искать запрос в мониторе и разбираться, но если все нормально, то рассмотреть опцию поднять ограничение для этой задачи в конфиге
- ждать зависимости - нужно понять, какая зависимость тупит, и возможно, поставить соответствующий тикет в MSTAT (или другую инстанцию)
- падать - нужно найти в мониторе или логах соответствующий `Exception` и либо поставить тикет на разбирательство (скажем, в YQL), либо считать ситуацию временно допустимой и обернуть `Exception` в `edera.ExcusableError`

#### yamarec_log_parsers

> Какие-то маркетные страницы сменили URL.

Открываем `/var/log/yandex/yamarec_log_parsers/monrun.log` и смотрим, проверка каких URL упала.
При необходимости обновляем регулярки в пакете `yandex-yamarec-log-parsers`.

#### rt-logger-delay*

> Тормозит заливка логов в базу.

Пока с этим ничего толком сделать нельзя. Только грустить. Изучаем детально вопрос в [специальном тикете](https://st.yandex-team.ru/MARKETRECOM-1007).

График заливки: https://market-graphite.yandex-team.ru/dashboard/#yamarec-rt-logger.

#### yamarec-rt-logger*

> Возникают ошибки в работе yandex-yamarec-rt-logger

Если получили ошибку "process doesn't exist, process 999999 not found" - проверяем запущен ли сервис yandex-yamarec-rt-logger. Запускаем сервис с помощью https://r.market.yandex-team.ru/

### Графики DT YT

[seneca-myt](https://solomon.yandex-team.ru/?project=yt&cluster=seneca-myt&service=yt_node_rpc&method=QueryService.Execute&aggregation=max&sensor=yt.rpc.server.request_time.total&user=-&graph=auto&checks=-Aggr%3BAggr_DC_Man%3BAggr_DC_Myt%3BAggr_DC_Sas&filter=top&filterBy=max&filterLimit=10&stack=false&b=2018-04-17T08%3A14%3A39.135Z&e=2018-04-17T21%3A46%3A10.661Z&l.host=n0035-myt%7Cn0036-myt%7Cn0037-myt%7Cn0038-myt%7Cn0039-myt) и [seneca-sas](https://solomon.yandex-team.ru/?project=yt&cluster=seneca-sas&service=yt_node_rpc&method=QueryService.Execute&aggregation=max&sensor=yt.rpc.server.request_time.total&user=-&graph=auto&checks=-Aggr%3BAggr_DC_Man%3BAggr_DC_Myt%3BAggr_DC_Sas&filter=top&filterBy=max&filterLimit=10&stack=false&b=2018-04-17T08%3A14%3A39.135Z&e=2018-04-17T21%3A46%3A10.661Z&l.host=n0036h%7Cn0037h%7Cn0038h%7Cn0039h%7Cn0040h).

### Если решился подкрутить лампочку

Есть два рода источника:
- сервисы могут настраивать периодические проверки с помощью конфига monrun, вроде [этого](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/yamarec/deploy/yandex-yamarec1/etc/monrun/yandex-yamarec1.conf)
- сервисы могут писать какую-нибудь статистику в логи
  - [LogShatter](https://github.yandex-team.ru/market-infra/market-health/tree/master/logshatter/src/main/java/ru/yandex/market/logshatter/parser/yamarec) их затем парсит, превращая в записи Clickhouse
  - [Clickphite](https://github.yandex-team.ru/market-infra/market-health/tree/master/config-cs-clickphite/src) конфигурируется превращать записи Clickhouse в метрики Graphite

По источникам настраиваются проверки и уведомления:
- [Ansible](https://github.yandex-team.ru/cs-admin/ansible-juggler-configs/blob/master/playbooks/market_recommendation.dev.yml) конфигурируется генерить конфиги для Juggler из проверок monrun и метрик Graphite
- [Juggler](https://juggler.yandex-team.ru/?query=host%3Dmarket_recommendation.dev) формирует по конфигам лампочки
- JugglerSearchBot отправляет уведомления в Telegram в соответствии с [настройками уведомлений](https://juggler.yandex-team.ru/notification_rules/?query=host%3Dmarket_recommendation.dev)

Старайся подкручивать пороги и прочие правила так, чтобы минимизировать долю шума и риск продолбать серьезный факап.
