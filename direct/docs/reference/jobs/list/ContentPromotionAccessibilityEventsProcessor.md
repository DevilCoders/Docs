## ContentPromotionAccessibilityEventsProcessor

### Продукт/подсистема

Баннеры типа продвижение контента - `ppc.banners.type = 'content_promotion'`


### Роль в работе продукта/подсистемы

Баннеры типа "продвижение контента" ссылаются на некоторый "контент" из внешней системы, информация о котором лежит в таблице [content_promotion](https://direct-dev.yandex-team.ru/db/ppc/tables/content_promotion.html). Контент сам по себе может становиться доступным или недоступным, за это отвечает поле `is_inaccessible`. Когда контент становится недоступным, джоба отправляет баннер в модерацию по особому флоу (`circuit: content_accessibility_checker`) - по сути Директ сам отправляет в модерацию вердикт `No`, который модерация потом возвращает обратно. А когда контент становится доступным, Директ отправляет `Yes`, а модерация выставляют предыдущий реальный статус модерации.


### Датафлоу

Обычный модерационный процессор, только реагирует на изменения не в баннере, а в `ppc.content_promotion.is_inaccessible`

- ESS-процессор реагирует на изменения в `ppc.content_promotion.is_inaccessible`.
- Отправляет в Модерацию через LogBroker.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ContentPromotionAccessibilityEventsProcessor.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'contentpromotion.ContentPromotionAccessibilityEventsProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [Специальные логи модерации](https://direct.yandex.ru/logviewer#~(logType~'ess_moderation~form~(fields~(~'log_time~'cid~'pid~'bid~'action~'source~'success~'data~'span_id)~conditions~(action~'request~data~'*25content_accessibility_checker*25)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$) с фильтром по `circuit: content_accessibility_checker`


### Какая функциональность пострадает от отказа джобы

- Если контент по баннеру станет недоступным - баннер не остановится в БК.
- Если наоборот станет доступным - баннер не возобновит показы.


### Как пользователи (или команда) заметят проблему и через какое время

- Могут всплыть на показах баннеры, которые ведут на недоступные ресурсы.
- Не запустится баннер после возобновления показа контента.


### Контакты разработчиков и менеджеров

Разработчики: [Игорь Гердлер](https://staff.yandex-team.ru/gerdler), [Сергей Димитров](https://staff.yandex-team.ru/dimitrovsd)


### Желательное время исправления в случае поломки

В течение дня.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

Такие же как у типичных модерационных джоб.


### Дополнительно: тонкости и подводные камни

Отсутствуют.
