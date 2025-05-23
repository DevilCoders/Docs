# Juggler Integration

Данный документ описывает интеграцию сервисов Няни с [Джаглером](https://wiki.yandex-team.ru/sm/juggler/).

## Возможности {#ability}

В секции **Information → Monitoring Settings → Juggler Settings** можно настроить произвольное количество активных и пассивных проверок для инстансов сервиса.

После включения интеграции (переключатель **Is enabled**) появляется три секции:

* **List of tags to mark Juggler checks with** — список тегов, которые будут присвоены Juggler-проверкам. Теги могут быть использованы для, например, включения даунтаймов по фильтрам (см. [JUGGLER-1186](https://st.yandex-team.ru/JUGGLER-1186)) или группировки проверок в [дашборде Джаглера](http://juggler.yandex-team.ru/).
* **Juggler hosts** — список Juggler-хостов, на которые будут навешаны активные проверки.
**Важно:** Juggler-хосты двух сервисов не могут пересекаться.
* **Aggregated checks** — список агрегаторов.
Агрегатор состоит из трёх секций:
* параметры группировки. Если выбран чекбокс **per group**, сигналы для каждой gencfg-группы (если сервис использует `EXTENDED_GENCFG_GROUPS` в секции **Runtime → Instance**) или аллокации (в случае `EXTENDED_ALLOCATIONS`) будут агрегироваться по отдельности; аналогично работают чекбоксы **per auto tags** и **per shard**.
* тип и параметры агрегатора;
* **Aggregated Active Checks** — список агрегируемых активных проверок;
* **Aggregated Passive Checks** — список агрегируемых пассивных проверок.


Подробнее о списке агрегируемых проверок. В каждой проверке указывается:

* **Juggler hostname** — одно из тех, что указано в секции **Juggler hosts**;
* **Juggler service name** — должно быть уникально в рамках указанного Juggler-хоста;
* тип и параметры модуля активной проверки;
* **Notifications** — список нотификаций. Типы нотификаций и их параметры подробно описаны [в документации Джаглера](https://wiki.yandex-team.ru/sm/juggler/notifications/#podpiska).

В Няне доступны не все типы агрегаторов, проверок и нотификаций. Если каких-либо из них не хватает в Няне — стоит создать тикет в очереди [SWAT](https://st.yandex-team.ru/SWAT).

## UI {#ui}

Так проверки выглядят в интерфейсе (их можно произвольно скрывать и показывать):

![screenshot](https://jing.yandex-team.ru/files/sshipkov/Screen%20Shot%202015-11-20%20at%2017.48.57.d14dd4f.png)

Если хотя бы одна проверка находится в статусе CRIT, дашборд будет показан без возможности его скрыть.

По клику на проверку будет показана служебная информация о проверке.

## Детали реализации {#details}

Процесс обновления проверок в Джаглере запускается по одному из двух событий (однако, задержка может достигать пары минут до запуска процесса и нескольких минут до того, как проверки заработают нормально):

* обновились info-атрибуты сервера (а вместе с ними, вероятно, секция **Monitoring Settings**);
* поменялся активный снапшот runtime-атрибутов.

Проверки в Джаглере создаются с помощью ansible-juggler, в description у них можно увидеть метку вида `nanny-<service_id>`.

Проверкам в Джаглере присваиваются теги инстансов (реализовано в рамках [SWAT-2188](https://st.yandex-team.ru/SWAT-2188)).
