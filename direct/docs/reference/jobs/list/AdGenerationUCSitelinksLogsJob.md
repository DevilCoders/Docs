## AdGenerationUCSitelinksLogsJob

### Продукт/подсистема { #subsystem }

Генерация данных для рекомендаций.


### Роль в работе продукта/подсистемы { #role }

Собираем и парсит логи от сервиса генерации данных, выгружает данные и статистику по дням.


### Датафлоу

- Запускается раз в сутки
- Читает дату последнего запуска JOBS_AD_GENERATION_UC_SITELINKS_LAST_START
- Ищет логи таблицы с логами директа [//home/direct/logs/messages_log](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/logs/messages_log), начиная даты с последнего запуска включительно и до вчерашнего дня включительно.
- Если таблиц для обработки нет, то завершение работы и время последнего запуска не перезаписывается.
- Для каждой таблицы запускается [sql-скрипт](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/adgeneration/ucsitelinks.sql?rev=8268697), который находит сообщения, парсит их, обрабатывает, считает статистику и выгружает на yt в [//home/direct/logs/ad_generation/UC/sitelinks/byDays/YYYY-MM-DD](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/logs/ad_generation/UC/sitelinks/byDays) подробные данные и добавляет в [//home/direct/logs/ad_generation/UC/sitelinks/summary](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/logs/ad_generation/UC/sitelinks/summary) статистику за день.
- Обновляет время последнего запуска.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dchecks_auto.direct.yandex.ru%26service%3Djobs.AdGenerationUCSitelinksLogsJob.working.production)
- [Логи](https://direct.yandex.ru/logviewer/short/v2/3964802957301099993) - не забудь изменить дату!


### Какая функциональность пострадает от отказа джобы { #affect }

Перестанут появляться данные за новые дни в статистике рекомендаций на [дашборде Мастера кампаний](https://datalens.yandex-team.ru/ov6o054zjb80i-master-kampaniy-uc-v-direkte?tab=KLZ&state=dbaaee73456).


### Как пользователи (или команда) заметят проблему и через какое время? { #appeal }

Менеджеры или аналитики могут заметить отставание подневных графиков в течение недели.


### Контакты разработчиков и менеджеров { #contacts }

Разработчики: [Саша Дубов](https://staff.yandex-team.ru/a-dubov) <br/>
Менеджеры: [Ксюша Аникеева](https://staff.yandex-team.ru/anyksenya) (Универсальные Кампании)


### Желательное время исправления в случае поломки { #time-to-fix }

Починить желательно в ближайшие несколько дней, до недели.


### Способы регулирования работы джобы

PpcProperty JOBS_AD_GENERATION_UC_SITELINKS_LAST_START хранит дату последнего успешного запуска.
Чтобы поставить джобу на паузу можно выставить дату в будущем. При этом, чтобы досчитать все пропущенные данные, нужно вернуть дату обратно. Данные за 1 день обрабатываются примерно 15 минут, поэтому не стоит ставить паузу больше чем на неделю, иначе пересчет данных займет более 2 часов.


### Известные причины поломок { #contacts }

- Недоступность hahn.


### Дополнительно: тонкости и подводные камни
