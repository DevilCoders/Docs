## yandex-market-mproxy

Это прокси-сервис, работающий на L4-уровне. Умеет:
* Распределять трафик между несколькими приемниками в зависимости от лимита на RPS, повешенного на каждый
* Зеркалировать все пакеты от клиента на один или более приемников

#### tcp-mirror
Принцип работы: mproxy принимает входящее соединение и поднимает коннект в сторону основной целевой системы.
Параллельно с этим поднимаются tcp-коннекты до одного, или более зеркал.
Все входящие от клиента сегменты данных пересылаются как на основную целевую систему, так и на все зеркала. 
Ответы основной цели отдаются клиенту, ответы зеркал игнорируются.
Если основная цель ответила раньше зеркал и закрыла соединение – соединения с зеркалами закрываются не дожидаясь их ответа.

### tcp-rps-balancer
Входящее от клиента tcp-соединение проксируется на на цель с минимальным идентификатором.
Если RPS-бюджет цели превышен (число новых соедиений, которое цель готова принять за одну секунду) – соединение проксируется на следующую цель.
Если RPS-бюджет цели не указан – она примет все соединения, которые до нее дойдут.

#### Healthchecks
Все цели мониторятся с запрошенной частотой на предмет доступности. Для проверки доступности можно использовать http-ручку.

#### SSL
Для http-mirror и http-rps-balancer (а также для healthcheck'а с помощью http-ping) можно включить ssl.
Для этого нужно прописать `proxy.<id>.use_target_ssl = true` или `proxy.<id>.use_mirror_ssl = true`.
Действует это на target- и на mirror-бекэнды соответственно.


#### Headers
Если mproxy работает в http-режиме, то можно модифицировать запросы, добавляя к ним свои заголовки вот так:
`proxy.<id>.target_header.<key> = <value>`. Соответственно вместо `target` может быть `mirror`. `value` должно быть без кавычек.

#### Исключение запросов из rps
Если не хочется, чтобы какие-то запросы не считались в rps, то укажите regexp для uri, по которому их надо выкидывать:
`proxy.<id>.exclude_regexp = <regexp>`. По умолчанию это `/ping`.

#### Пример конфигурации с двумя секциями: зеркалирующей и rate-limit'ирующей:
```
management.port = 8006
management.address = 127.0.0.1

# Зеркало на 2 ноды
proxy.25498.type = tcp-mirror
proxy.25498.listen.address = fdee:fdee:0:3400:0:3c9:0:60
proxy.25498.listen.port = 17000
proxy.25498.target.1.address = sas2-5321-ba6-sas-market-prep--d10-17050.gencfg-c.yandex.net
proxy.25498.target.1.port = 17050
proxy.25498.target.2.address = sas1-1743-a4e-sas-market-prod--4a2-17050.gencfg-c.yandex.net
proxy.25498.target.2.connection_attempts = 2
proxy.25498.target.2.connection_close_delay = 0
proxy.25498.target.2.port = 17050
proxy.25498.target.2.timeout = 100
proxy.25498.target.3.address = vla2-8193-68c-vla-market-prod--c40-17050.gencfg-c.yandex.net
proxy.25498.target.3.connection_attempts = 2
proxy.25498.target.3.connection_close_delay = 0
proxy.25498.target.3.port = 17050
proxy.25498.target.3.timeout = 100

# rate-limit: 100 rps на первый узел, 200 на второй, остальное на последний
proxy.example2.type = tcp-rps-balancer
proxy.example2.listen.address = fdee:fdee::3400:0:3c9:0:60
proxy.example2.listen.port = 17048
proxy.example2.target.1.address = vla2-8193-68c-vla-market-prod--c40-17050.gencfg-c.yandex.net
proxy.example2.target.1.port = 17049
proxy.example2.target.1.max_rps = 100
proxy.example2.target.2.address = vla2-8194-68c-vla-market-prod--c40-17050.gencfg-c.yandex.net
proxy.example2.target.2.port = 17049
proxy.example2.target.2.max_rps = 200
proxy.example2.target.3.address = vla2-8195-68c-vla-market-prod--c40-17050.gencfg-c.yandex.net
proxy.example2.target.3.port = 17049
```

##### Пример управления инстансом
* Посмотреть вю конфигурацию
```
curl -sS http://localhost:8006/proxy
```
* Посмотреть конфигурацию секции 25498
```
curl -sS http://localhost:8006/proxy/25498
```
* Изменить лимит RPS у второго узла секции example2
```
curl -X PUT http://localhost:8006/proxy/example2/2/max_rps/400
```
* Выгрузить и загрузить ранее сохраненную конфигурацию разом:
```
curl -sS http://localhost:8006/proxy | grep max_rps > /tmp/config
curl -X POST -H "Content-Type: text/plain" --data-binary "@/tmp/config" http://localhost:8006/load
``
* Получить текущую статистику
```
curl -sS http://localhost:8006/stats
```

### links

[sandbox job to build debian package](https://sandbox.yandex-team.ru/task/273474812/view)
