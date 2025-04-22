## UpdatePagePlaceJob

### Продукт/подсистема

[Внутренняя реклама (aka Банана)](../../../glossary/glossary.md#internal-ads).


### Роль в работе продукта/подсистемы

Импортирует связи площадки (`page_id`) с местом (`place_id`) из YT в MySQL. Используется для отображения мультиклиентной статистики (в базе это клиент, а во внутренней рекламе под ним скрывается продукт - Я.Музыка, Я.Карты), где есть фильтрация по пейджам, и по ним бэкенд должен найти кампании. У кампаний внутренней рекламы есть только place_id, поэтому нужна связка page_id и place_id, чтобы найти по пейждам нужные кампании.


### Датафлоу

- Читает все записи для пейджей внутренней рекламы из таблицы в YT [//home/yabs/dict/PageSlotSequence](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/yabs/dict/PageSlotSequence). Выбирается наиболее свежая таблица из кластеров: `HAHN`, `ARNOLD`.
- В таблицу MySQL добавляет недостающие записи [ppcdict.page_place](https://direct-dev.yandex-team.ru/db/ppcdict/tables/page_place.html)
- Удаляет из MySQL записи, которых больше нет в YT'е


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.UpdatePagePlaceJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'internal.UpdatePagePlaceJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Не получиться фильтровать в мультиклиентной статистике по новым пейджам, для которых джоба не успела импортировать связку с `place_id`.


### Как пользователи (или команда) заметят проблему и через какое время

Заметят на странице мультиклиентной статистики при фильтрации по новым пейджам, для которых джоба не успела импортировать связку с `place_id`.


### Контакты разработчиков и менеджеров

Разработчики: [Бехруз Афзали](https://staff.yandex-team.ru/xy6er), [Захар Зибаров](https://staff.yandex-team.ru/zakhar) <br/>
Менеджеры: [Ваня Пахомов](https://staff.yandex-team.ru/irpakhomov), [Марина Ежова](https://staff.yandex-team.ru/ezhova-m)


### Желательное время исправления в случае поломки

Ждет неделю, а может и дольше, т.к. новые пейджы добавляются оч редко и тем реже по ним срочна нужна фильтрация.


### Способы регулирования работы джобы

- ppc-property `page_place.last_update_unix_time` — содержит время последнего обновления данных [YT-таблицы](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/yabs/dict/PageSlotSequence), для которого джоба успешно завершила импорт. Можно указать дату из прошлого, если джоба неверно импортировала данные, и после починки джобы их нужно заново импортировать. Дата сравнивается с атрибутом таблицы `max_unix_time`.



### Известные причины поломок




### Дополнительно: тонкости и подводные камни
