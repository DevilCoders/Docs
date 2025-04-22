## MobileAppsIosSkadNetworkSlotsJob

### Продукт/подсистема

Реклама мобильных приложений.


### Роль в работе продукта/подсистемы

Назначает слоты в базе в таблице [ios_skadnetwork_slots](https://direct-dev.yandex-team.ru/db/ppcdict/tables/ios_skadnetwork_slots.html) для кампаний в рамках [SkAdNetwork](https://developer.apple.com/documentation/storekit/skadnetwork).


### Датафлоу

- Джоба освобождает слоты занятые остановленными кампаниями.
- Джоба освобождает слоты занятые неверифицированными приложениями.
- Джоба назначает доступные слоты новым кампаниям.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.MobileAppsIosSkadNetworkSlotsJob.working.production&last=1DAY&query=)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'mobileappsiosskadnetworkslots.MobileAppsIosSkadNetworkSlotsJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Новые РМП кампании не будут получать слоты, из-за этого у них будет некорректно собираться статистика в БК.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи не увидят статистику для новых РМП кампаний с активированным флагом `SkAdNetwork`.


### Контакты разработчиков и менеджеров

Разработчики: [Егор Иватько](https://staff.yandex-team.ru/ivatkoegor), [Захар Зибаров](https://staff.yandex-team.ru/zakhar) <br/>
Менеджеры: [Роман Кухта](https://staff.yandex-team.ru/kuhtich)


### Желательное время исправления в случае поломки

Как можно быстрее.


### Способы регулирования работы джобы



### Известные причины поломок



### Дополнительно: тонкости и подводные камни
