# Events-log

Эта библиотека отвечает за events-log (он же front-log).

Помимо Яндекс.Метрики и маркетинговых счётчиков у auto.ru есть собственный лог событий, с которым работают фронт и аппы. Мы скармливаем в ручку [/events/log/](http://autoru-api-server.vrts-slb.test.vertis.yandex.net/swagger/?url=/api-docs#!/events/logEvents) различные события, а аналитики могут потом выстроить по ним произвольную выборку и проверить различные гипотезы.

## Данные для логирования событий
[VERTISMETA-151](https://st.yandex-team.ru/VERTISMETA-151)
Прежде чем добавить и прокинуть любой новый параметр, убедись что его поддержали на беке.
Потому что бек не пропустит его молча, а вернёт ошибку.
Актуальный формат данных, которые готов принять бек, можно смотреть в proto-модели [stat-events](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/auto/api/stat_events.proto) в [schema-registry](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/).

## Тестирование
Отслеживать отправку событий с клиента можно через devtools/Network, запросы в `/-/ajax/[ package ]/events_log/`.
Так как поле `events` это json в виде строки, для удобства дебага во внутренней сети Яндекса его содержимое логируется в консоль с префиксом `[events-log]`.
