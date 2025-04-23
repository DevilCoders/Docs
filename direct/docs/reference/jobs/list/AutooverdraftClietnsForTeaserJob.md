## AutooverdraftClietnsForTeaserJob

### Продукт/подсистема

Деньги.


### Роль в работе продукта/подсистемы

Выгрузка клиентов, которым доступна возможность уходить в минус на счёте (автоовердрафт), но которые его не включили. Используется для включения клиентам тизера через Я.Аудитории.


### Датафлоу

- Делает [yql-запрос](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/autooverdraft/autooverdfart_clients_for_teaser.yql) в выгрузку базы директа в YT на кластерах Hahn, Arnold.
- Результат сохраняет в [//home/direct/export/autooverdraft_clients_for_teaser](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/autooverdraft_clients_for_teaser) на соответствующем кластере (Выгрузки: Hahn, Arnold).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.AutooverdraftClietnsForTeaserJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'autooverdraft.AutooverdraftClietnsForTeaserJob~service~'direct.jobs)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- Операции в YQL (актуальная ссылка будет в логах джобы)


### Какая функциональность пострадает от отказа джобы

- Клиенты будут видеть в интерфейсе неактуальные тизеры о возможности включения автоовердрафта.
- Джоба [AutoOverdraftEmailSenderJob](AutoOverdraftEmailSenderJob.md) перестанет отправлять письма.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи будут жаловаться на неактуальные тизеры об автоовердрафте (включили, а тизер остался; автоовердрафт недоступен, а тизер показывается и т. п.)


### Контакты разработчиков и менеджеров

Разработчики: [Сергей Гукасьян](https://staff.yandex-team.ru/gukserg), [Михаил Иволгин](https://staff.yandex-team.ru/mivolgin)


### Желательное время исправления в случае поломки

Сутки.


### Способы регулирования работы джобы

-


### Известные причины поломок

- Проблемы с доступностью кластеров Hahn, Arnold.
- Изменения в синтаксисе YQL-запросов.


### Дополнительно: тонкости и подводные камни

-
