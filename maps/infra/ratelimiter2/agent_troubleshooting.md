
## Вижу на графиках 429ки. Как понять кого блокируем?
На панели рейтлимитера для сервиса можно посмотреть графики RPS клиентов и расхода квот.  
Панели создаются автоматически с URL-ом в формате: `https://yasm.yandex-team.ru/template/panel/<project_id>-ratelimiter2-panel`  
project_id - название подпапки в конфигурации квот [maps/config/ratelimiter/](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter)

Подробности про заблокированные запросы нужно искать в `/var/log/nginx/error.log` (рейтлимитер банит запросы на nginx).  
Например:
```
/var/log/nginx/error.log на driving-router

[error] 941#941: *468892 [lua] rate-limiter2-nginx-plugin.lua:34: rate_access(): Limit EXCEEDED for 2017679 to maps-core-driving-router, client: 2a02:6b8:c10:3782:0:45d1:6af7:0, server: router.maps.yandex.ru, request: "GET /v2/route?mode=approx&lang=ru-RU&origin=yataxi&rll=30.459228%2C50.382571~30.528580%2C50.401634 HTTP/1.1", host: "core-driving-router.maps.yandex.net"
[error] 941#941: *473238 [lua] rate-limiter2-nginx-plugin.lua:34: rate_access(): Limit EXCEEDED for 2017679 to maps-core-driving-router, client: 2a02:6b8:c11:20a:0:45d1:641a:0, server: router.maps.yandex.ru, request: "GET /v2/route?mode=approx&lang=ru-RU&origin=yataxi&rll=55.217375%2C51.746007~55.133418%2C51.719108 HTTP/1.1", host: "core-driving-router.maps.yandex.net"
[error] 939#939: *472951 [lua] rate-limiter2-nginx-plugin.lua:34: rate_access(): Limit EXCEEDED for 2017679 to maps-core-driving-router, client: 2a02:6b8:c11:e0a:0:45d1:89b7:0, server: router.maps.yandex.ru, request: "GET /v2/route?mode=approx&lang=ru-RU&origin=yataxi&rll=30.457798%2C50.383685~30.528580%2C50.401634 HTTP/1.1", host: "core-driving-router.maps.yandex.net"
```


## Вижу на графиках 403ки. Тут замешан рейтлимитер?
Нулевая квота в рейтлимитере это явный запрет доступа к ресурсу для клиентов.
Запросы, которые блокируются такой квотой, завершаются с кодом 403.  

Детали можно увидеть в `/var/log/nginx/error.log`.
Например:
```
[2020-04-14 13:25:59] <nginx 414> warning: ratelimiter2 forbidden: Reject XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX to maps_mobile_offline_caches@free
[2020-04-14 13:26:00] <nginx 414> warning: ratelimiter2 forbidden: Reject XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX to maps_mobile_offline_caches@free
[2020-04-14 13:26:01] <nginx 411> warning: ratelimiter2 forbidden: Reject XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX to maps_mobile_offline_caches@free
```

## Где заданы квоты моего сервиса? Хочу отредактировать
Квоты задаются через конфигурацию в аркадии: [maps/config/ratelimiter](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter).  
Для каждого сервиса заводится отдельная папка с yaml конфигами для стейджингов.  
**NB:** Рекомендуем дождаться исполнения прекоммитных проверок.  
По коммиту CI запустит задачу, которая загрузит новые квоты на сервер (в почту придет два письма от sandbox задач MAPS_RATE_LIMITS_REFRESHER и MAPS_RATE_PANELS_REFRESHER).  
После чего, в течении 5-ти минут обновление распространится на все подключенные машины.

## Горят мониторинги ratelimiter-proxy-*
Горящие мониторинги означают потерю связности в пайплайне `nginx-plugin <-> ratelimiter-proxy <-> ratelimiter-server`.  
В этом случае деградирует синхронизация счетчиков на разных машинах кластера. Негативный эффект тут в том, что рейтлимитер будет пропускать больше запросов чем нужно.  
Также отваливается обновление конфигурации лимитов на затронутых хостах.  

Деградация связности рейтлимитера не приводит к блокировке лишних запросов.

Проведите первичную диагностику проблемы, рекомендации приведены ниже для каждого мониторинга.  
Если ситуация не прояснилась и нужна помощь, то проконсультируйтесь [у нас](https://abc.yandex-team.ru/services/maps-core-ratelimiter).

### ratelimiter-proxy-alive и ratelimiter-proxy-load
Не стартует локальный сервант агента рейтлимитера (ratelimiter-proxy).  
Счетчики не синхронизуюется между разными nginx worker-ами.  
Также нет синхронизации счетчиков с сервером.  
Хост не получает обновления лимитов.

Диагностика неполадок в логе серванта: `/var/log/yandex/maps/ratelimiter-proxy/ratelimiter-proxy.log`

### ratelimiter-proxy-sync-upstream:
Агент долгое время не синхронизирует счетчики с сервером.

Поищите ошибки в логе агента: `/var/log/yandex/maps/ratelimiter-proxy/ratelimiter-proxy.log`  
Вероятнее всего причина в потере связи конкретного хоста с внешним миром.


### ratelimiter-proxy-counter_sync-* и ratelimiter-proxy-resources_limits_get-*
Nginx-плагин рейтлимитера не может связаться с локальным агентом (сервант ratelimiter-proxy) для синхронизации счетчиков / обновления лимитов.

Диагностику причин нужно искать:
- Со стороны плагина в `/var/log/nginx/error.log`
- Со стороны серванта в `/var/log/yandex/maps/ratelimiter-proxy/ratelimiter-proxy.log`

## Что-то пошло не так, хочу срочно отключить.
Аварийный способ отключить агент рейтлимитера на отдельной машине:
1) Способ A: отключить плагин рейтлимитера в nginx.  
    Это жесткий способ, так как он перезагружает nginx и рвет существующие конекшны клиентов. Зато он гарантировано отключает блокировку запросов рейтлимитером.  

    При помощи agent-ctl скрипта:  
    `/usr/lib/yandex/maps/ratelimiter2/agent-ctl.sh disable`  
    Для отключения на всем кластере, используйте executer.  
    **Внимание:** agent-ctl скрипт делает `nginx -s reload`, рекомендуем делать p_exec по дц. 

    Когда разобрались в неполадках, не забудьте включить обратно:  
    `/usr/lib/yandex/maps/ratelimiter2/agent-ctl.sh enable`

2) Способ B: остановить сервант локального агента (ratelimiter-proxy).  
    Это сравнительно безболезненный способ, не затрагивает работу nginx, но не даёт 100% гарантии от блокировок рейтлимитером. Эффективен чтобы мгновенно отключить секундные квоты (точнее уменьшить их влияние во много раз).  
    `yacare stop ratelimiter-proxy`  
    Отключит синхронизацию счетчиков между worker-ами nginx, каждый worker будет считать квоты по-отдельности вместо суммы для всего кластера.  
    Но nginx-плагин продолжит работать и в теории может блокировать запросы (например если уже съедена daily квота).

    Чтобы включить обратно:  
    `yacare start ratelimiter-proxy` 
