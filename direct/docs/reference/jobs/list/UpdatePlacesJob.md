## UpdatePlacesJob

### Продукт/подсистема

[Внутренняя реклама (aka Банана)](../../../glossary/glossary.md#internal-ads).


### Роль в работе продукта/подсистемы

Импортирует параметры плейсов из YT в MySQL. Информация о плейсах используется в разных местах Внутренней рекламы, но больше всего нужен при создании новой кампании.


### Датафлоу

- Читает все записи из таблицы в YT [//home/yabs/dict/Place](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/yabs/dict/Place). Выбирается наиболее свежая таблица из кластеров: `HAHN`, `ARNOLD`.
- В таблицу MySQL [ppcdict.internal_ad_places](https://direct-dev.yandex-team.ru/db/ppcdict/tables/internal_ad_places.html) добавляются недостающие записи.
- Обновляются записи, которые были в MySQL, но изменились в YT'е.
- Удаляются из MySQL записи, которых больше нет в YT'е.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.UpdatePlacesJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'internal.UpdatePlacesJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Станет невозможным создание кампании для нового плейса, который джоба не успела импортировать.


### Как пользователи (или команда) заметят проблему и через какое время

На странице создания кампаний в саджесте по плейсам не будет нового плейса, который джоба не успела импортировать.


### Контакты разработчиков и менеджеров

Разработчики: [Бехруз Афзали](https://staff.yandex-team.ru/xy6er), [Захар Зибаров](https://staff.yandex-team.ru/zakhar) <br/>
Менеджеры: [Ваня Пахомов](https://staff.yandex-team.ru/irpakhomov), [Марина Ежова](https://staff.yandex-team.ru/ezhova-m)


### Желательное время исправления в случае поломки

В среднем починка ждет неделю. т.к. новые плейсы добавляются редко.


### Способы регулирования работы джобы

- ppc-property `places.last_update_unix_time` — содержит время последнего обновления данных [YT-таблицы](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/yabs/dict/Place), для которого джоба успешно завершила импорт. Можно указать дату из прошлого, если джоба неверно импортировала данные, и после починки джобы их нужно заново импортировать. Дата сравнивается с атрибутом таблицы `max_unix_time`.


### Известные причины поломок




### Дополнительно: тонкости и подводные камни
