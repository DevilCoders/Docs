## AdGenerationUCImagesLogsJob


{% include [subsystem](AdGenerationUCSitelinksLogsJob.md#subsystem) %}


{% include [role](AdGenerationUCSitelinksLogsJob.md#role) %}


### Датафлоу

- Запускается раз в сутки
- Читает дату последнего запуска JOBS_AD_GENERATION_UC_IMAGES_LAST_START
- Ищет логи таблицы с логами директа [//home/direct/logs/messages_log](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/logs/messages_log), начиная даты с последнего запуска включительно и до вчерашнего дня включительно.
- Если таблиц для обработки нет, то завершение работы и время последнего запуска не перезаписывается.
- Для каждой таблицы запускается [sql-скрипт](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/adgeneration/ucimages.sql?rev=8268697), который находит сообщения, парсит их, обрабатывает, считает статистику и выгружает на yt в [//home/direct/logs/ad_generation/UC/images/byDays/YYYY-MM-DD](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/logs/ad_generation/UC/images/byDays) подробные данные и добавляет в [//home/direct/logs/ad_generation/UC/images/summary](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/logs/ad_generation/UC/images/summary) статистику за день.
- Обновляет время последнего запуска.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dchecks_auto.direct.yandex.ru%26service%3Djobs.AdGenerationUCImagesLogsJob.working.production)
- [Логи](https://direct.yandex.ru/logviewer/short/v2/3968111462495065330) - не забудь изменить дату!


{% include [affect](AdGenerationUCSitelinksLogsJob.md#affect) %}


{% include [appeal](AdGenerationUCSitelinksLogsJob.md#appeal) %}


{% include [contacts](AdGenerationUCSitelinksLogsJob.md#contacts) %}


{% include [contacts](AdGenerationUCSitelinksLogsJob.md#time-to-fix) %}


### Способы регулирования работы джобы

PpcProperty JOBS_AD_GENERATION_UC_IMAGES_LAST_START хранит дату последнего успешного запуска.
Чтобы поставить джобу на паузу можно выставить дату в будущем. При этом, чтобы досчитать все пропущенные данные, нужно вернуть дату обратно. Данные за 1 день обрабатываются примерно 15 минут, поэтому не стоит ставить паузу больше чем на неделю, иначе пересчет данных займет более 2 часов.


### Известные причины поломок

- Недоступность hahn.


### Дополнительно: тонкости и подводные камни
