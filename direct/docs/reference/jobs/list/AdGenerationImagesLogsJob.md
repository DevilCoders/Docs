## AdGenerationImagesLogsJob


{% include [subsystem](AdGenerationUCSitelinksLogsJob.md#subsystem) %}


{% include [role](AdGenerationUCSitelinksLogsJob.md#role) %}


### Датафлоу

- Запускается раз в сутки
- Читает дату последнего запуска JOBS_AD_GENERATION_IMAGES_LAST_START
- Ищет логи таблицы с логами директа [//home/direct/logs/messages_log](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/logs/messages_log), начиная даты с последнего запуска включительно и до вчерашнего дня включительно.
- Если таблиц для обработки нет, то завершение работы и время последнего запуска не перезаписывается.
- Для каждой таблицы запускается [sql-скрипт](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/adgeneration/images.sql?rev=8268697), который находит сообщения, парсит их, обрабатывает, считает полезность и выгружает на yt в [//home/direct/logs/ad_generation/images/1d/suggest/YYYY-MM-DD](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/logs/ad_generation/images/1d/suggest) рекомендации и в [//home/direct/logs/ad_generation/images/1d/apply/YYYY-MM-DD](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/logs/ad_generation/images/1d/apply) данные о сохраненных картинках и оценка полезности рекомендаций.
- Обновляет время последнего запуска.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dchecks_auto.direct.yandex.ru%26service%3Djobs.AdGenerationImagesLogsJob.working.production)
- [Логи](https://direct.yandex.ru/logviewer/short/v2/4285663916534617955) - не забудь изменить дату!


### Какая функциональность пострадает от отказа джобы

Перестанут появляться данные за новые дни в статистике рекомендаций [дашборде Картинок](https://datalens.yandex-team.ru/pnv50oigxzpuj-kartinki).


### Как пользователи (или команда) заметят проблему и через какое время?

Менеджеры или аналитики могут заметить отставание подневных графиков в течение недели.


{% include [contacts](AdGenerationUCSitelinksLogsJob.md#contacts) %}


{% include [contacts](AdGenerationUCSitelinksLogsJob.md#time-to-fix) %}


### Способы регулирования работы джобы

PpcProperty JOBS_AD_GENERATION_IMAGES_LAST_START хранит дату последнего успешного запуска.
Чтобы поставить джобу на паузу можно выставить дату в будущем. При этом, чтобы досчитать все пропущенные данные, нужно вернуть дату обратно. Данные за 1 день обрабатываются примерно 15 минут, поэтому не стоит ставить паузу больше чем на неделю, иначе пересчет данных займет более 2 часов.


### Известные причины поломок

- Недоступность hahn.


### Дополнительно: тонкости и подводные камни
