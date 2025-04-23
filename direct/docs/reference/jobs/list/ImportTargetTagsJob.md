## ImportTargetTagsJob

### Продукт/подсистема

Кампании с фиксированным CPM (прайсовые кампании, `ppc.campaigns.type = 'cpm_price'`).


### Роль в работе продукта/подсистемы

Таргет-тег (еще иногда называют ПИ-тегом) - множество страниц (пейджей, `Page`) в терминах Партнерского Интерфейса.

В прайсовых кампаниях менеджер при заведении прайсового пакета/продукта (таблица [ppcdict.cpm_price_packages](https://direct-dev.yandex-team.ru/db/ppcdict/tables/cpm_price_packages.html)) указывает подмножество таргет-тегов, из которых потом пользователь будет выбирать те, на которые он хочет нацелиться. Данная джоба забирает актуальный список таргет-тегов из таблицы в YT от Партнерского интерфейса и перекладывает их в MySql Директа, чтобы потом отображать на странице заведения пакета.


### Датафлоу

- Читает все данные из таблицы в YT в директории: [//home/partner/dict/target_tags](https://yt.yandex-team.ru/hahn/navigation?path=//home/partner/dict/target_tags).
- Обновляет таблицу [ppcdict.target_tags](https://direct-dev.yandex-team.ru/db/ppcdict/tables/target_tags.html) -  добавляет и обновляет данные, но не удаляет.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ImportTargetTagsJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'dataimport.ImportTargetTagsJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

У пользователей - никакая. У менеджеров - не будут появляться новые таргет-теги, но они появляются очень редко.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи - никак и никогда, менеджеры могут заметить.


### Контакты разработчиков и менеджеров

Разработчики: [Максим Серебряков](https://staff.yandex-team.ru/palasonic), [](https://staff.yandex-team.ru/aliho) <br/>
Партнёрский интерфейс: [Роман Зуев](https://staff.yandex-team.ru/zurom)


### Желательное время исправления в случае поломки

Дни. Новые таргет теги появляются редко и используются менеджерами.


### Способы регулирования работы джобы

Отсутствуют.


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Отсутствуют.
