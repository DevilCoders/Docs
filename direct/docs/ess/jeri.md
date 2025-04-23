[Концепция](concept.md)

[Разработка ESS контура](howto-code.md)

# Эксплуатация ESS Директа

TDB

Пока заглушка с полезными ссылками:
* [Продовый топик binlogbroker-а](https://lb.yandex-team.ru/lbkx/accounts/direct/direct-ppcdata-binlog-log)
* [Продовые топики ESS](https://lb.yandex-team.ru/lbkx/accounts/direct/ess)
* [Дашборд ESS в Solomon-е](https://solomon.yandex-team.ru/?project=direct&dashboard=ess&project=direct&cluster=app_binlogbroker&service=java-monitoring&env=production)
* [Дашборд ESS в Solomon-е для ТС](https://solomon.yandex-team.ru/?project=direct-test&cluster=app_binlogbroker&service=java-monitoring&env=testing&dashboard=ess-test&b=36m40s&e=)

# Чёрный список ESS

Через [internal tools](https://direct.yandex.ru/internal_tools/#ess_blacklist_add_tool) можно добавлять объекты в чёрный список по полям logicObject-а.  
Ess-обработчик для объектов удовлетворяющих чёрному списку не будет вызываться.

Стоит учитывать, что можно фильтровать не по всем полям объекта, а только по тем, что попадают в топик.
Для AggregatedStatusEventObject запись в топике выглядит например ([посмотреть в логвьювере](https://nda.ya.ru/t/SPqLJMQ2469KdL)) так:
```json
{"cid":"null", "deleted":"true", "id":"478343751", "parent_id":"null", "type":"CAMPAIGN"}
```
Это значит, что для фильтрации по номеру кампании — нужно фильтровать по полю `id`, а не `cid`.

## Тест для самопроверки { #selftest }

Для самопроверки можно ответить на несколько вопросов: [ссылка](https://forms.office.com/Pages/ResponsePage.aspx?id=91gB6oFweEaw7X55tD91WioDI29cj_FKvM5f4YSFsflUNlY3NDY0Q0lXQkpYM0hOVERZQlg5UVQ2WS4u)

Если опросник не показывается, залогинься по [инструкции](../guide/basics/howto-office-com-login.md)
