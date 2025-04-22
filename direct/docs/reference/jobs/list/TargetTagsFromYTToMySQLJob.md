## TargetTagsFromYTToMySQLJob
### Продукт/подсистема




### Роль в работе продукта/подсистемы
Прогнозатору требуется определять кампании с фиксированным CPM как кампании по рекламе
недвижимости или auto.ru для составления более точного прогноза. Данная джоба обновляет
список актуальных тегов для капаний, по которым требуется отдавать данные прогнозатору.


### Датафлоу
- Берет список строк target_tags из realty_target_tags и autoru_target_tags
- Составляет строку из этого списка через запятую.
- Если длина не превышает максимальный размер поля text в MySQl, то перезаписывает значение в таблице ppc_properties где name="inventori_target_tags".


### Способы наблюдения за текущим состоянием
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.TargetTagsFromYTToMySQLJob.working.production)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'inventoribookedtargettags.TargetTagsFromYTToMySQLJob.java)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы
В случае изменения списка тегов для объявлений по недвижимости и автору,
прогнозатор не будет получать некоторые кампании для составления точного прогноза.



### Как пользователи (или команда) заметят проблему и через какое время



### Контакты разработчиков и менеджеров

Разработчики: [Кулаков Александр](https://staff.yandex-team.ru/alex-kulakov) <br/>


### Желательное время исправления в случае поломки
Несколько дней.



### Способы регулирования работы джобы



