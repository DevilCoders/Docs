## WalletsWarningsEmailSenderJob

### Продукт/подсистема
Отправка пользователям писем о том, что деньги скоро закончатся



### Роль в работе продукта/подсистемы
Джоба отправляет пользователю два письма:
1. На общем счете осталось денег меньше чем на 3 дня показов
2. На общем счете осталось денег меньше чем на 1 день показов




### Датафлоу
Читает из БД данные кошельков, фильтрует, отправляет письма через Рассылятор, обновляет статус в БД.
<details>
<summary>Подробнее</summary>
- Получаем из базы PPC кампании-кошельки по которым были оплаты и по которым, возможно, нужно отправить письмо об окончании средств.<br/>
- Учитываем только кошельки с выключенным автопополнением и дефолтным пороговым значением уровня остатка средств на кампании для отсылки уведомления  (поле money_warning_value таблицы <a href="https://direct-dev.yandex-team.ru/db/ppc/tables/camp_options.html">ppc.camp_options</a>, дефолтное значение: 20% )<br/>
- Фильтруем полученные кошельки по фиче NEW_WALLET_WARNINGS_ENABLED, оставляем только те, где фича включена<br/>
- Получаем дополнительные данные по кампаниям и пользователям<br/>
- Из динамической таблицы БК <a href="https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/yabs/stat/OrderStatDay">OrderStatDay</a> получаем суммарные траты по всем кампаниям клиента за последнюю неделю<br/>
- Считаем средний расход за день и за три дня по последней неделе, сравниваем с текущей суммой на Общем счете и принимаем решение об отправке соответствующего письма с учетом остатка на Общем счете и статуса statusMail в таблице <a href="https://direct-dev.yandex-team.ru/db/ppc/tables/campaigns.html">ppc.campaigns</a><br/>
- Отправляем письма через Рассылятор<br/>
- При успешной отправке письма меняем статус statusMail в таблице <a href="https://direct-dev.yandex-team.ru/db/ppc/tables/campaigns.html">ppc.campaigns</a><br/>
</details>


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.WalletsWarningsEmailSenderJob.working.production&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'walletswarnings.WalletsWarningsEmailSenderJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы
Клиенты перестанут получать письма о том, что деньги скоро закончатся



### Как пользователи (или команда) заметят проблему и через какое время
Пользователи возможно будут жаловаться на то, что их не предупредили о том, что деньги скоро закончатся



### Контакты разработчиков и менеджеров

Разработчики: [Сергей Гукасьян](https://staff.yandex-team.ru/gukserg) <br/>
Менеджеры: [Ярослав Михайлов](https://staff.yandex-team.ru/yarmikh)


### Желательное время исправления в случае поломки
Чинить в течение суток под присмотром app-duty




### Способы регулирования работы джобы
Джоба не регулируется



### Известные причины поломок




### Дополнительно: тонкости и подводные камни
Параллельно джобе аналогичные уведомления отправляет перловый скрипт [ppcSendOrderWarnings.pl](https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/protected/ppcSendOrderWarnings.pl)
Перловый скрипт отправляет письма тем, у кого нет кошелька или не включена фича NEW_WALLET_WARNINGS_ENABLED или установлен отличный от дефолтных 20% пороговый уровень  для отсылку уведомления о малом остатке средств на кампании.
