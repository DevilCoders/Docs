## CanvasOperationsOnCreativesJob

### Продукт/подсистема

Канвас (Canvas), работа с креативами.


### Роль в работе продукта/подсистемы

(Фактически является ваншотом).

Аналог [внутреннего инструмента для работы с креативами](https://test-direct.yandex.ru/internal_tools/#canvas_on_creatives_operation) для массового применения. Например, для добавления нового поля в VAST всех креативов.


### Датафлоу

- Из ppc_properties читает настройку `JOBS_CANVAS_OPERATIONS_ON_CREATIVES_RANGES` в которой хранятся [параметры](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/java/ru/yandex/direct/jobs/canvasoperationsoncreatives/model/VideoCreativesRangesList.java) текущего запуска.
- На основе этих параметров выбирает идентификаторы креативов из базы.
- Вызывает соответствующие ручки в канвасе с полученными идентификаторами.


### Способы наблюдения за текущим состоянием

- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'canvasoperationsoncreatives.CanvasOperationsOnCreativesJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Зависит от причины запуска.


### Как пользователи (или команда) заметят проблему и через какое время?

Логи, косвенные наблюдения - скриншоты не переснялись и т.п.


### Контакты разработчиков и менеджеров

Разработчик: [Егор Иватько](https://staff.yandex-team.ru/ivatkoegor) + тот, кто запустил <br/>
Менеджер: [Алексей Александров](https://staff.yandex-team.ru/hrustyashko)


## Желательное время исправления в случае поломки

Как правило не критично, но зависит от кейса.


## Способы регулирования работы джобы

Читает [параметры](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/java/ru/yandex/direct/jobs/canvasoperationsoncreatives/model/VideoCreativesRangesList.java) текущего запуска из ppc-property `JOBS_CANVAS_OPERATIONS_ON_CREATIVES_RANGES` (фильтр по типам креативов, диапазоны идентификаторов креативов для каждого шарда и размеры пачек для запросов в базу и канвас).



## Известные причины поломок

Таймауты в ручках канваса.


## Дополнительно: тонкости и подводные камни
