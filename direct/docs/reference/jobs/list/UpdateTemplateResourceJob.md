## UpdateTemplateResourceJob

### Продукт/подсистема

[Внутренняя реклама (aka Банана)](../../../glossary/glossary.md#internal-ads).


### Роль в работе продукта/подсистемы

Импортирует из YT в MySQL параметры ресурсов шаблонов (параметры полей баннеров внутренней рекламы). Информация о ресурсах используется в разных местах внутренней рекламы, но больше всего нужна при создании/редактировании баннеров.


### Датафлоу

- Читает все записи из таблицы в YT [//home/yabs/dict/TemplateResource](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/yabs/dict/TemplateResource). Выбирается наиболее свежая таблица из кластеров: `HAHN`, `ARNOLD`.
- В MySQL в таблицу [ppcdict.template_resource](https://direct-dev.yandex-team.ru/db/ppcdict/tables/template_resource.html) добавляются недостающие записи.
- Обновляются записи, которые были в MySQL, но изменились в YT'е.
- Удаляются из MySQL записи, которых больше нет в YT'е.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.UpdateTemplateResourceJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'internal.UpdateTemplateResourceJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Создание/редактирование баннеров для ресурсов, по которым были изменения, но джоба не успела их импортировать.


### Как пользователи (или команда) заметят проблему и через какое время

На странице создания/редактирования баннеров будет неактуальная информация по ресурсам, например не будет новых.


### Контакты разработчиков и менеджеров

Разработчики: [Бехруз Афзали](https://staff.yandex-team.ru/xy6er), [Захар Зибаров](https://staff.yandex-team.ru/zakhar) <br/>
Менеджеры: [Ваня Пахомов](https://staff.yandex-team.ru/irpakhomov), [Марина Ежова](https://staff.yandex-team.ru/ezhova-m)


### Желательное время исправления в случае поломки

В среднем починка ждет неделю. т.к. ресурсы меняются не так часто.


### Способы регулирования работы джобы

- ppc-property `template_resource.last_update_unix_time` — содержит время последнего обновления данных [YT-таблицы](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/yabs/dict/TemplateResource), для которого джоба успешно завершила импорт. Можно указать дату из прошлого, если джоба неверно импортировала данные, и после починки джобы их нужно заново импортировать. Дата сравнивается с атрибутом таблицы `max_unix_time`.


### Известные причины поломок




### Дополнительно: тонкости и подводные камни
