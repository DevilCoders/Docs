## UpdateTemplatePlaceJob

### Продукт/подсистема

[Внутренняя реклама (aka Банана)](../../../glossary/glossary.md#internal-ads).


### Роль в работе продукта/подсистемы

Импортирует связи шаблонов внутренней рекламы (`templateId`) с плейсами (`placeId`), где эти шаблоны могут размещаться. Связка шаблона с плейсом используется много где, больше всего нужно при создании баннеров. По плейсу кампании показываются доступные шаблоны для создания баннера.


### Датафлоу

- Читает все записи для пейджей внутренней рекламы из таблицы в YT [//home/yabs/dict/TemplatePlace](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/yabs/dict/TemplatePlace). Выбирается наиболее свежая таблица из кластеров: `HAHN`, `ARNOLD`.
- В таблицу в MySQL [ppcdict.template_place](https://direct-dev.yandex-team.ru/db/ppcdict/tables/template_place.html) добавляются недостающие записи.
- Из MySQL удаляются записи, которых больше нет в YT'е.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.UpdateTemplatePlaceJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'internal.UpdateTemplatePlaceJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Функциональность создания баннеров внутренней рекламы будет ограничена: не получится создать баннеры по новым шаблонам, для которых джоба не успела импортировать связку с плейсом.


### Как пользователи (или команда) заметят проблему и через какое время

На странице создания баннеров не получиться выбрать новые шаблоны, для которых джоба не успела импортировать связку с плейсом. Пользователи - наши маркетологи, и знают про новые шаблоны и плейсы.


### Контакты разработчиков и менеджеров

Разработчики: [Бехруз Афзали](https://staff.yandex-team.ru/xy6er), [Захар Зибаров](https://staff.yandex-team.ru/zakhar) <br/>
Менеджеры: [Ваня Пахомов](https://staff.yandex-team.ru/irpakhomov), [Марина Ежова](https://staff.yandex-team.ru/ezhova-m)


### Желательное время исправления в случае поломки

Ждет неделю, а может и дольше, т.к. новые шаблоны и связка с плейсом добавляются редко.


### Способы регулирования работы джобы

- ppc-property `template_place.last_update_unix_time` — содержит время последнего обновления данных [YT-таблицы](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/yabs/dict/TemplatePlace), для которого джоба успешно завершила импорт. Можно указать дату из прошлого, если джоба неверно импортировала данные, и после починки джобы их нужно заново импортировать. Дата сравнивается с атрибутом таблицы `max_unix_time`.


### Известные причины поломок




### Дополнительно: тонкости и подводные камни
