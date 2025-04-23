## InvalidYandexServicesDomainsMonitoringJob

### Продукт/подсистема

Рекламирование сервисов Яндекса.


### Роль в работе продукта/подсистемы

На большинство сервисов Яндекса ведут ссылки вида `https://yandex.ru/<service_name>`, поэтому домен вычисляется как `yandex.ru`. А мы хотим, чтобы домен вычислялся так: для `yandex.ru/maps/` -> `maps.yandex.ru`.

Джоба нужна для того чтобы узнавать о появлении в баннерах ссылок на новые сервисы, для которых нужно внести в код особое правило вычисления домена.


### Датафлоу

- Читает из таблицы `ppc.banners` баннеры, рекламирующие сервисы Яндекса, последовательно во всех шардах.
- Отправляет уведомление о найденных "неправильных" доменах и новых сервисах.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.InvalidYandexServicesDomainsMonitoringJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'banner.InvalidYandexServicesDomainsMonitoringJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Ответственные не будут вовремя узнавать о появлении новых сервисов и "направильных" доменах. Фактически, сейчас так и происходит, и жалоб не слышно.


### Как пользователи (или команда) заметят проблему и через какое время

Увидят в рекламной выдаче неправильный домен.


### Контакты разработчиков и менеджеров

Разработчики: [](https://staff.yandex-team.ru/) <br/>
Менеджеры: [](https://staff.yandex-team.ru/)


### Желательное время исправления в случае поломки

Чинить в ZBP, приоритет должен определить менеджер поддержки.


### Способы регулирования работы джобы

- Ppc-property `YANDEX_SERVICES_WITHOUT_SPECIAL_DOMAIN` — список сервисов Яндекса, про которые менеджеры знают и для которых не нужен специальный домен.
- Ppc-property `YANDEX_URL_TO_SERVICE_MAPPINGS` — мапа, где ключ - первый сегмент пути в урле, значение - домен сервиса.


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Логика находится в `BannersUrlHelper.extractHostFromHrefWithWwwOrNull`.
