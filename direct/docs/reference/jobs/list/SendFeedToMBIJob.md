### Продукт/подсистема

Товарная реклама(Смарты, ДО, Фиды в ТГО).

### Роль в работе продукта/подсистемы

Регистрирует фиды и хосты в MBI, для дальнейшей прокачки фидов с них в DataCamp.

### Датафлоу

Достает из MySQL фиды, которые не были зарегистрированы в MBI, по пачке правил и фичей отбирает те, что надо
зарегистрировать.<br />
Дергает ручки MBI для регистрации(пока что ручки не батчевые).

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&last=1DAY&service=jobs.SendFeedToMBIJob.working.production)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'feed.SendFeedToMBIJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)

### Какая функциональность пострадает от отказа джобы

Если фиды/хосты не будут регистрироваться в MBI, то тогда их офферы не будут прокачиваться в DataCamp, оттуда они не
смогут попасть в маркетный индекс или в BannerLand, и в итоге часть рекламы клиента может отображаться нецеликом,
устареть или не показываться вообще.

### Как пользователи (или команда) заметят проблему и через какое время

Жалобы на старые данные в смартах/ДО, на отсутствие товарной галереи или смартов/ДО

### Контакты разработчиков и менеджеров

Разработчики: [buhter](https://staff.yandex-team.ru/buhter) <br/>
Менеджеры: [ulyashevda](https://staff.yandex-team.ru/ulyashevda)

### Желательное время исправления в случае поломки

Максимально оперативно.
