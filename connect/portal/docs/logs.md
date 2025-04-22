## Логи в Коннекте

#### Логи в Кибане

- [Логи всех воркспейсных проектов в Кибане](https://logs.ws.yandex-team.ru)
- [Документация по синтаксису запросов](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)

Чтобы выбрать логи по конкретному проекту и окружению, нужно выбрать в выпадушке вверху левой колонки интересующее окружение. Например, для продакшена Коннекта это `logs__workspace-portal-prod_*`. В правом верхнем углу можно выбрать время, за какое должны показываться логи. По умолчанию - последние 15 минут.

Пример запроса для получения debug-логов для ошибок за последние 15 минут:

```
https://logs.ws.yandex-team.ru/app/kibana?#/discover?_g=(refreshInterval:(display:Off,pause:!f,value:0),time:(from:now-15m,mode:quick,to:now))&_a=(columns:!(message,'@fields.body','@fields.login'),index:'logs__workspace-portal-prod_*',interval:auto,query:(query_string:(analyze_wildcard:!t,query:'@fields.error:true%20AND%20@fields.level:debug')),sort:!('@timestamp',desc))
```


#### Логи в интерфейсе Qloud

Заходим в [приложение в Qloud](https://qloud-ext.yandex-team.ru/projects/workspace/portal), выбираем окружение и переходим на вкладку Logs.

Здесь не удастся посмотреть подробные логи, так что этим вариантом нужно пользоваться, когда сломались логи в Кибане.


#### Локальные логи

В каждом контейнере хранятся локальные логи.

Как их посмотреть:

- Заходим в нужное окружение в [Qloud](https://qloud-ext.yandex-team.ru) и кликаем на кнопку "Details" в компоненте "back"
- Выбираем адреса хостов из описания (например, `i-f8244f848bc7.qloud-c.yandex.net`) и заходим в каждый из них по ssh
- Логи лежат в файле `/var/log/yandex-connect/all.log`

Если не удалось получить доступ по ssh к контейнеру, нужно проверить доступ через [puncher](https://puncher.yandex-team.ru). Там же можно этот доступ заказать.
