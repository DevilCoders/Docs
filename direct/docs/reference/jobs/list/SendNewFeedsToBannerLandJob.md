### Продукт/подсистема
Товарная реклама(Смарты, ДО, Фиды в ТГО).


### Роль в работе продукта/подсистемы
Отправляет новые фиды в Bannerland, в зависимости от типа фида, это или отправка на парсинг фида или только "валидация".
"Валидация" происходит при любой отправке, от BL получаем информацию, валиден ли фид, кол-во офферов в нем,
дерево категорий, список вендоров и превью.


### Датафлоу
Клиенты создают новый фиды или редактируют уже существующий, так или иначе в `ppc.feeds` появляется запись с
`update_status = New`. Такие фиды, джоба должна отправить в BmApi, ручку yml2directInf
Результатом должен быть переход фида в статус `Done` или `Error`, и заполнение полей
и связанных таблиц фидов(`ppc.perf_feed_history`, `ppc.perf_feed_vendors`, `ppc.perf_feed_categories`).
За одну итерацию на одном шарде джоба набирает до `default_feed_to_bannerland_iteration_capacity` фидов(по умолчанию 5)
и в параллель делает долгие синхронные запросы в BmApi(таймаут — 1 час или для некоторых клиентов выше,
кому разрешены фиды большего объема)

### Способы наблюдения за текущим состоянием
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&last=1DAY&service=jobs.SendNewFeedToBannerLandJob.working.production)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'feed.SendNewFeedToBannerLandJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)

### Какая функциональность пострадает от отказа джобы
Новые и отредактированные фиды перестанут отправляться в BL и валидироваться.<br/>
В результате не будет происходить генерации баннеров по офферам этих фидов или будут использоваться устаревшие данные.

### Как пользователи (или команда) заметят проблему и через какое время
На гриде фидов будут видны зависшие в статусе `New` фиды. <br/>
Реклама или не будет откручиваться или будет неактуальной

### Контакты разработчиков и менеджеров

Разработчики: [buhter](https://staff.yandex-team.ru/buhter), [ali-al](https://staff.yandex-team.ru/ali-al) <br/>
Менеджеры: [ulyashevda](https://staff.yandex-team.ru/ulyashevda)


### Желательное время исправления в случае поломки
Максимально оперативно.


### Способы регулирования работы джобы
Есть пропертя `default_feed_to_bannerland_iteration_capacity`: кол-во фидов обрабатываемых за одну итерацию, по умолчанию — 5


### Известные причины поломок
—


### Дополнительно: тонкости и подводные камни
—
