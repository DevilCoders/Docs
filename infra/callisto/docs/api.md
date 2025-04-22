## API

**Раздатчик конфигов**

Доступен по адресам `http://{man,sas,vla}-configs-cajuper.n.yandex-team.ru`
* `/configs/<host>/<port>` -- конфиг инстанса


**Сборщик отчетов**

Доступен по адресам `http://{man,sas,vla}-reports-v2-cajuper.n.yandex-team.ru`

Выбор формата отчётов осуществляется через стандартный HTTP заголовок Accept, поддерживаются следующие значения:
* `application/json` Формат JSON, используется по умолчанию.
* `application/message` Формат MessagePack
* `application/protobuf` [protobuf](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/reports/proto/report.proto)

(V1 отчетница deprecated, доступна тут `http://sas-reports-cajuper.n.yandex-team.ru`, используется только adv)
* `/report/<host>/<port>` -- отчет инстанса
* `/with_tags` -- все отчеты
* `/with_tags?tag=<tag1>&tag=<tag2>...` -- все отчеты, в которых встречается каждый из указанных тегов
    - [Пример](https://sas-reports-v2-cajuper.n.yandex-team.ru/with_tags?tag=SAS_WEB_DEPLOY)
* `/uptime` -- сколько секунд прошло с первого полученного отчета
* `/info/requests_count` -- счетчик числа запросов


**Контроллеры**

Правильный способ сделать api: добавить своему контроллеру ?handler=<path> ручку
(смотри про ручку set_handler в code.md)

Deprecated ручки:
* `/status` -- общая информация о состоянии контроллера
* `/view/build_progress/<tier_name>` -- где какой шард строится/построился
* `/view/deploy_progress/<tier_name>` -- где какой шард скачивается/скачался (tier_name необязательный параметр)
* `/view/searchers_state/<slot_name>` -- над чем "летят" базовые (slot_name необязательный параметр)
* `/info/loop_statistics` -- информация о работе контроллера
