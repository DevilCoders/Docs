## ReceiveModerationResponseJob

### Продукт/подсистема

Интеграция с Модерацией.


### Роль в работе продукта/подсистемы

Приём вердиктов из Модерации по всем типам рекламных объектов.


### Датафлоу

- Читает поток сообщений из LogBroker. Топик прописан в [common-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/resources/common-production.conf) в секции `moderation_service.logbroker.response.topic`.
- В зависимости от типа объекта, для которого пришло сообщение, вызывает разные обработчики. Каждый обработчик реализует собственную логику: обычно сохраняет результат модерации только в MySQL, но может и обращаться к соседним сервисам. Например `BannerstorageCreativeModerationResponseHandler` обращается к API BannerStorage.
- Так же пишет в специальный лог ess-moderation.

### Способы наблюдения за текущим состоянием

- [Дэшборд нового транспорта с модерацией](https://solomon.yandex-team.ru/?project=direct&dashboard=ess-moderation&project=direct&cluster=app_java-jobs&service=java_jobs&env=production&b=2021-03-03T04%3A54%3A44.034Z&e=2021-03-03T16%3A54%3A44.034Z).
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ReceiveModerationResponseJob.working.production&query=&last=1DAY).
- [Лог транспорта с Модерацией (ess-moderation)](https://direct.yandex.ru/logviewer/#~(logType~'ess_moderation~form~(fields~(~'log_time~'cid~'pid~'bid~'action~'source~'success~'data~'span_id)~conditions~(action~'response~source~'response)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$) - возможные значения полей лога можно посмотреть в классе [ModerationLogEntry](https://a.yandex-team.ru/arc/trunk/arcadia/direct/common/src/main/java/ru/yandex/direct/common/log/container/ModerationLogEntry.java).
- [Лог джобы](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'moderation.ReceiveModerationResponseJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$).


### Какая функциональность пострадает от отказа джобы

Перестанем принимать вердикты. Баннеры будут ожидать модерации и не уедут в показы. Очередь будет расти.


### Как пользователи (или команда) заметят проблему и через какое время

Максимально критично. Пользователи увидят, что их баннеры и другие модерируемые объекты (в том числе отдельные ресурсы баннеров) долго находятся в статусе "На модерации".


### Контакты разработчиков и менеджеров

Разработчики:  [Игорь Костромин](https://staff.yandex-team.ru/elwood),  [Денис Говорков](https://staff.yandex-team.ru/oxid) <br/>
Менеджеры: [Алексей Александров](https://staff.yandex-team.ru/hrustyashko)


### Желательное время исправления в случае поломки

Максимально оперативно.


### Способы регулирования работы джобы

Отсутствуют.


### Известные причины поломок

- Падения в обработки запросов, в том числе при обращении во внешний сервисы (BannerStorage, Solomon).
- Не-запуск джобы шедулером.
- Проблемы чтения данных из логброкера.


### Дополнительно: тонкости и подводные камни
