## AutoOverdraftEmailSenderJob

### Продукт/подсистема

Деньги.


### Роль в работе продукта/подсистемы

Отправляет пользователю письмо с сообщением о том, что ему доступен автоовердрафт.


### Датафлоу

- Использует выгрузку клиентов с доступным автооведрафтом в YT - [//home/direct/export/autooverdraft_clients_for_teaser](https://yt.yandex-team.ru/arnold/navigation?path=//home/direct/export/autooverdraft_clients_for_teaser), которую формирует джоба [AutooverdraftClietnsForTeaserJob](AutooverdraftClietnsForTeaserJob.md) (Hahn, Arnold).
- Выбирает дополнительные данные из базы ppc по клиентам.
- Отправляет пользователям письма через Рассылятор.
- После успешной отправки письма устанавливает флаг `auto_overdraft_notified` в поле `client_flags` таблицы [ppc.clients_options](https://direct-dev.yandex-team.ru/db/ppc/tables/clients_options.html) .


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.AutoOverdraftEmailSenderJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'autooverdraft.AutoOverdraftEmailSenderJob~service~'direct.jobs)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Пользователи перестанут получать письма о доступности автоовердрафтов.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи скорей всего никак не заметят. Возможно заметят менеджеры, если посмотрят в выгрузку в рассыляторе или логи


### Контакты разработчиков и менеджеров

Разработчики: [Александр Дуплищев](https://staff.yandex-team.ru/ppalex), [Кирилл Богданов](https://staff.yandex-team.ru/sco76), [Михаил Иволгин](https://staff.yandex-team.ru/mivolgin)


### Желательное время исправления в случае поломки

Сутки.


### Способы регулирования работы джобы

Можно отключить отправку писем в рассыляторе.


### Известные причины поломок

Недоступность YT (Hahn, Arnold), проблемы с базами Директа, недоступность Рассылятора.


### Дополнительно: тонкости и подводные камни

Иногда [Михаил Иволгин](https://staff.yandex-team.ru/mivolgin) может просить выключить джобу при изменении логики начисления автоовердравта в Балансе чтобы клиентов не спамили письмами.
