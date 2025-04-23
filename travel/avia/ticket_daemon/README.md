internal_ticket_daemon - Демон опроса партнеров
======================================

Сервис по опросу авиакомпаний и агентов, с целью получения цен на перелеты из
точки А в точку B.

# Как запустить на dev машинке
Копируем настройки
```bash
cp tools/samples/environments.sh tools/environments.sh
vim tools/environments.sh
```

Секреты
`AVIA_TICKET_DAEMON_SECRETS_*`, `AVIA_TICKET_DAEMON_PARTNER_PROXY_LOGIN`, `AVIA_TICKET_DAEMON_PARTNER_PROXY_PASSWORD`
нужно брать из тестинга:
```bash
ssh root@ticket-daemon.xxxxxxxxx.sas.yp-c.yandex.net
env | grep AVIA_TICKET_DAEMON_SECRETS_
env | grep AVIA_TICKET_DAEMON_PARTNER_PROXY_
```
!!! **Эти секреты никуда не надо выкладывать/коммитить** \
Так же некоторые другие настройки содержат значение `see readme`. Их выставляете в зависимости от вашего дев окружения \
Убедитесь, что настройки `TICKET_DAEMON_CACHEROOT` совпадают между внутреннем сервисов и его api \

`YT_TOKEN` можно получить [тут](https://oauth.yt.yandex.net/)

Чтобы подключаться к реплике MySQL, надо добавить `AVIA_TICKET_DAEMON_MYSQL_HOST=c-<CLUSTER-ID>.ro.db.yandex.net`.
`CLUSTER-ID`, а также `DATABASE_NAME` и `USER` можно получить в [YC](https://yc.yandex-team.ru/folders/foo1262pmfvsq72flh90/managed-mysql?section=list)
(или в тестинге, тогда см. выше).

## Запускаем:
```bash
./tools/run-dev.sh                      # запустить приложение
./tools/run-shell.sh                    # запустить python manage.py
ya make -tt                             # запустить тесты
./tools/run-aggregate-min-prices-celery # запустить celery для расчета мин цен
```

## Опрос партнера (cli)
На разработческой машине:

```
$ ./tools/tickets-query-partner.sh -h
$ ./tools/tickets-query-partner.sh -p booktripruag -f s9600215 -t s9623562 -d 2020-11-16 -R -n ru -l ru
```

В проде:
```
Y_PYTHON_ENTRY_POINT='travel.avia.ticket_daemon.tools.tickets_query_partner:main' /app/app  -p anywayanyday -f c65 -t c2 -d 2021-10-22 -b 2021-11-02 -R -n ru -l ru
```

## Модуль опроса партнера

Подробнее [тут](https://a.yandex-team.ru/arc_vcs/travel/avia/ticket_daemon/ticket_daemon/partners/README.md)

## Проверка изменений в модуле партнёра с тестового фронта

Для проверки изменений в модуле партнёра с тестового фронта, можно пойти вот сюда

https://front.avia.tst.yandex.kz/experiments

и в поле ```force-ticket-daemon-host``` вписать свой dev, или стендовый хост. Аналогично можно использовать другие национальные домены (```.com, .com.tr, .ua```),
но нельзя использовать ```.ru```. Пример того, как указать стендовый хост:

```http://pr-2076002.ticket-daemon-stands.testing.avia.yandex.net```


## Сборка образа руками
ya package ./pkg.json --docker

## Release-machine
https://rm.z.yandex-team.ru/component/ticket_daemon/manage

## Sentry
[Production](https://sentry.production.avia.yandex.net/sentry/production-ticket-daemon) \
[Testing](https://sentry.testing.avia.yandex.net/sentry/testing-ticket-daemon/) \

## Документация
[Формат лога avia_variatns](./ticket_daemon/lib/yt_loggers/avia_variants.md)

#### Убедиться что задачи отправляются в очередь
```bash
tail -f log/main/ticket_daemon/daemon/variants_saver.log \
    | grep "Set task query_aggregate_min_prices_task"
```

#### Убедиться что задачи выполняются воркером
```bash
tail -f ./log/main/ticket_daemon/daemon/tasks.log
```

## Запуск локального редиса

Установить redis
```bash
sudo apt-get install redis-server
```

Запуск
```bash
~/redis-stable/src/redis-server
```

Запуск в режиме sentinel
```bash
~/redis-stable/src/redis-server ~/redis-stable/sentinel.conf --sentinel
```

В ~/redis-stable/sentinel.conf нужно указать хост для мастера, в example конфиге(~/redis-stable/sentinel.conf) уже прописан localhost

```
sentinel monitor mymaster 127.0.0.1 6379 1
```
