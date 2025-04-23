## LastAvailableDateFetcher

### Продукт/подсистема

Статистика и отчеты.


### Роль в работе продукта/подсистемы

Определяет максимально возможную дату отчета для агентских оффлайн-отчетов (которые строятся джобой [AgencyOfflineReportBuilder](AgencyOfflineReportBuilder.md)) — она прокидывается в интерфейс и использутся при валидации.


### Датафлоу

- По наличию таблиц в YT определяет самую позднюю дату, за которую можно заказать отчёт.
- Сохраняет полученную дату в ppc-property `AGENCY_OFFLINE_REPORT_MAX_DATE`.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.LastAvailableDateFetcher.working.production&last=1DAY&query=)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'service~'method~'span_id~'message)~conditions~(service~'direct.jobs~method~'agencyofflinereport.LastAvailableDateFetcher)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Пропадет возможность указать свежие даты (например вчера/позавчера) при заказе оффлайн-отчета.


### Как пользователи (или команда) заметят проблему и через какое время

Через пару дней — то что свежие даты будут недоступны в селекторе дат.


### Контакты разработчиков и менеджеров

Разработчики: [Александр Дуплищев](https://staff.yandex-team.ru/ppalex) <br/>
Менеджеры: [Мария Савицкая](https://staff.yandex-team.ru/mariabye)


### Желательное время исправления в случае поломки

День - два.


### Способы регулирования работы джобы

Никаких.


### Известные причины поломок

YT-кластер `Hahn` недоступен.


### Дополнительно: тонкости и подводные камни
