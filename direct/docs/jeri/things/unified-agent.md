# Unified Agent

Unified Agent -- Яндексовая разработка; программа (демон, агент) для приема и пересылки логов, метрик и т.п.
Может принимать сообщения по протоколам syslog и grpc.
Отправляет сообщения в LogBroker.

В Директе используется в ЯДеплойных приложениях для сбора и распределения логов.

Конфиги искать в подах в каталоге `/etc/yandex/unified_agent/conf.d/`

Основные сущности, которыми оперирует конфиг:
- входы (input)
- выходы (output)
- фильтры (filter)
- хранилища (storage)
- цепочки преобразований (pipe)
- каналы (channel)
- маршруты доставки (route)

Подробнее о них можно узнать в документации unified agent.
Вкратце: в конфиге маршрутами доставки соединить входы с каналами, которые ведут к каким-то выходам. Грубо соотношение сущностей можно представить так:
```
route = input + channel
channel = pipe + (output|channel|fanout|case)
fanout|case = channel + channel + ...
pipe = (storage|filter) + (storage|filter) + ...
```
fanout и case -- настройки канала для размножения потока или выбора канала по условию. Подробнее см. документацию по конфигурированию channel.

Документация по unified agent: <https://logbroker.yandex-team.ru/docs/unified_agent>

