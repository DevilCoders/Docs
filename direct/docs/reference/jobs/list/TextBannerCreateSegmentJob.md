## TextBannerCreateSegmentJob

### Продукт/подсистема

Сбор сегментов аудиторий ([подробнее](../../product/segments.md)).


### Роль в работе продукта/подсистемы

Автоматическое создание сегментов аудиторий в Я.Аудиториях из пользователей, видевших ТГО рекламу в РСЯ.


### Датафлоу

- Берет из [ppc.video_segment_goals](https://direct-dev.yandex-team.ru/db/ppc/tables/video_segment_goals.html) пачку записей об уже созданных сегментах с самой старой датой обновления.
- Читает id уникальных пользователей из промежуточных табличкек [//home/direct/segments/common/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/segments/common/1d) 
- Создаем по этим id сегменты через API Я.Аудиторий.
- Обновляет данные в табличке в MySQL.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.TextBannerCreateSegmentJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'common.TextBannerCreateSegmentJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Не блокирует основные сценарии, но функциональность важна для пользователей, особенно крупных: сегменты аудиторий перестанут пополняться новыми пользователями, видевшими рекламу.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи через день-два увидят, что размер сегмента меньше, чем охват группы в статистике.


### Контакты разработчиков и менеджеров

Разработчики: [Азат Хузин](https://staff.yandex-team.ru/khuzinazat)


### Желательное время исправления в случае поломки

В течение дня.


### Способы регулирования работы джобы

- PpcProperty `segment_jobs_segments_limit` - размер пачки обрабатываемых за раз сегментов. Можно понизить в случае проблем с памятью.


### Известные причины поломок

Жрет слишком много памяти.


### Дополнительно: тонкости и подводные камни
