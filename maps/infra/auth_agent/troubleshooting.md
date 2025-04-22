### Горят мониторинги auth_agent-alive и auth_agent-load <a name="auth_agent_startup"></a>
Не стартует локальный сервант auth агента.  
Диагностика неполадок в логе серванта: `/var/log/yandex/maps/auth_agent/auth_agent.log`  

Вероятная причина - неправильно настроены параметры TVM для доступа в blackbox.  
Убедитесь, что в `/etc/tvmtool/tvmtool.conf` задан секрет и в секции **dsts** есть **blackbox** с правильным значением **dst_id**.   
Валидация окружения TVM и blackbox на старте серванта - стандартный механизм yacare, который предотвращает запуск с неправильными настройками.

**Внимание:** Если обслуживание залогиновых запросов это основной сценарий, то есть сервис без auth_agent неработоспособен. Рекомендуем в этом случае настроить проверку живости auth_agent в своей ручке /ping. Таким образом выкатка сервиса остановится при проблемах с auth_agent и балансеры не будут подавать нагрузку на нерабочие хосты.

Подробнее про конфигурацию auth_agent [в документации](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/auth_agent/README.md#auth_agent_setup).


### Горит мониторинг http-user_ticket-error и 500ки на графиках залогиновых ручек
Большое количество 500ок на ручке /user_ticket серванта auth_agent.

Убедитесь, что сервант auth_agent запущен. Диагностика проблем с запуском серванта [в соседней секции](#auth_agent_startup). 

Вероятные причины ошибок при работающем серванте - проблемы с грантами или ошибки на стороне blackbox.
Диагностика в логе серванта: `/var/log/yandex/maps/auth_agent/auth_agent.log`

Обратитесь [в чатик поддержки blackbox](https://t.me/joinchat/BfrKfRJHbU1vrrsfxUwLWQ)  
Дополнительно можно проконсультироваться в [Geo Helpline](https://t.me/joinchat/B0tVN0KnO40AS9GFVS-hSA) или напрямую в [инфраструктуре геосервисов](https://staff.yandex-team.ru/departments/yandex_content_geodev_5685).

**Автоматический fallback**: Если залогин для ваших запросов опциональный, то есть большинство ручек могут обслуживать запросы, если у них оторвать креденшлы пользователя (пример такого сценария - персонализация ответов пользователям).  
В этом случае переопределите обработчик `on_internal_error` плагина, чтобы игнорировать проблемы с blackbox и не прерывать обработку запроса ([подробнее в доке](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/auth_agent/README.md)).


### Подскочили тайминги http-user_ticket и на графиках залогиновых ручек
В нормальной ситуации тайминги составляют около 3-4мс в 95й квантили.

Вероятная причина - высокие тайминги запросов в blackbox из-за сетевых проблем на некоторых машинах или целой локации.

Закройте от траффика проблемные машины пока разбираетесь в причинах проседания связности.

Проконсультируйтесь [в чатике поддержки blackbox](https://t.me/joinchat/BfrKfRJHbU1vrrsfxUwLWQ)


### Горит мониторинг http-user_ticket-401
Всплеск запросов с пользовательскими креденшлами, которые не проходят авторизацию в blackbox.

Ответы blackbox можно посмотреть в логе серванта: `/var/log/yandex/maps/auth_agent/auth_agent.log`

Например:
```
[2020-04-21 07:25:39] warning: ::1 GET /user_ticket? => HTTP 401: Invalid account has been globally logged out response from: http://blackbox.yandex.net/blackbox?method=oauth
[2020-04-21 07:25:39] warning: ::1 GET /user_ticket? => HTTP 401: Invalid account has been globally logged out response from: http://blackbox.yandex.net/blackbox?method=oauth
[2020-04-21 07:25:39] warning: ::1 GET /user_ticket? => HTTP 401: Invalid account has been globally logged out response from: http://blackbox.yandex.net/blackbox?method=oauth
```

Небольшой фон 401ок - нормальное явление, связанное с разлогином пользователей и протуханием креденшлов.  
Возможно настроены слишком чувствительные пороги для мониторинга и стоит их поднять(в sedem_config). 

Но если ситуация выглядит необычно и тревожно, то проконсультируйтесь [в чатике поддержки blackbox](https://t.me/joinchat/BfrKfRJHbU1vrrsfxUwLWQ)
