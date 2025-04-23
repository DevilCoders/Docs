## UpdatePayForConversionPessimizedUsersJob

### Продукт/подсистема

Конверсионный автобюджет. Показ предупреждений о недостаточном количестве конверсий при открутках кампаний с оплатой за конверсии.

![Предупреждение о недостаточном количестве конверсий](_images/UpdatePayForConversionPessimizedUsersJob_1.png "Предупреждение о недостаточном количестве конверсий" =507x314)


### Роль в работе продукта/подсистемы

Если клиент использует в автостратегии низкоконверсионную или вовсе не достижимую цель, то такому клиенту будет предоставляться меньше рекламного трафика. Всех клиентов, использующих конверсионные стратегии, ОКР записывает в отдельную таблицу в YT, проставляя "коэффициент пессимизации" <= 1 (где 1 - хороший клиент :).

Джоба переносит из ОКР в Директ этот самый "коэффициент пессимизации".


### Датафлоу

- Читает из YT-таблицы [//home/ads/cpa_autobudget/multipliers/login2min_bid_tcpa_multiplier/stream/latest](https://yt.yandex-team.ru/arnold/navigation?path=//home/ads/cpa_autobudget/multipliers/login2min_bid_tcpa_multiplier/stream/latest) данные о клиентах, использующих конверсионные стратегии.
- Записывает "коэффициент пессимизации" в MySQL таблицу [ppcdict.cpa_autobudget_pessimized_users](https://direct-dev.yandex-team.ru/db/ppcdict/tables/cpa_autobudget_pessimized_users.html).
- Удаляет из таблицы [ppcdict.cpa_autobudget_pessimized_users](https://direct-dev.yandex-team.ru/db/ppcdict/tables/cpa_autobudget_pessimized_users.html) логины, отсутствующие в yt-таблице.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.UpdatePayForConversionPessimizedUsersJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'cpaautobudget.UpdatePayForConversionPessimizedUsersJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- Можно посмотреть время самой старой записи в табличке MySQL: `select min(update_time) from cpa_autobudget_pessimized_users;`


### Какая функциональность пострадает от отказа джобы

Данные о пессимизации логинов перестанут обновляться, вследствие чего мы будем показывать неактуальные предупреждения при редактировании автостратегий.


### Как пользователи (или команда) заметят проблему и через какое время

Для ранее пессимизированных пользователей мы будем показывать предупреждение (даже если они уже исправили проблему с конверсиями) <br/>
Для новых проблемных пользователей предупреждения показываться не будут.


### Контакты разработчиков и менеджеров

Разработчики: [Паша Новосёлов](https://staff.yandex-team.ru/pashkus), [Паша Рябов](https://staff.yandex-team.ru/pavryabov) <br/>
Менеджеры: [Таня Удалова](https://staff.yandex-team.ru/tudalova)


### Желательное время исправления в случае поломки

Данные в таблицах ОКР обновляются несколько раз раз в сутки.
Допустимо починить в течение дня, не дольше. Иначе это заметят пользователи.


### Способы регулирования работы джобы

Пишет дату последнего обновления в ppc-property `bs.update.pay_for_conversion_pessimized_users.last_update_time`.


### Известные причины поломок

Однажды со стороны ОКР закрыли доступ к таблице.


### Дополнительно: тонкости и подводные камни, известные вероятные причины поломки
