## SafeSearchTearOffPromocodesJob

### Продукт/подсистема

Часть системы антифрода для промокодов. Работа с промокодами Баланса, самим Балансом и Безопасным поиском (антифродом).


### Роль в работе продукта/подсистемы

По данным Безопасного поиска о том, что конкретные промокоды на конкретные кампании активированы фродерами, джоба инициирует отрыв промокодов в Балансе.


### Датафлоу

- Каждые 20 минут джоба берёт из ppc-property `FRAUD_PROMO_REDIRECTS_LAST_ROW` номер последней обработанной строчки в append-only таблице в [hahn.//home/antivir/prod/export/direct-promocodes/fraud_promo_redirects](https://yt.yandex-team.ru/hahn/navigation?path=//home/antivir/prod/export/direct-promocodes/fraud_promo_redirects).
- Читает из таблицы все следующие строки.
- Отрывает промокоды запросом в Баланс.
- Записывает самый большой последовательный (при параллельной обработке можем один раз зафейлить что-нибудь из середины) обработанный номер строки в вышеуказанной ppc-property.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.SafeSearchTearOffPromocodesJob.working.production&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'promocodes.SafeSearchTearOffPromocodesJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Фродеры будут крутить рекламу дальше бесплатно. Недополучение денег Директом.


### Как пользователи (или команда) заметят проблему и через какое время

Никак.


### Контакты разработчиков и менеджеров

Разработчики: [Кирилл Богданов](https://staff.yandex-team.ru/sco76), [Роман Кухта](https://staff.yandex-team.ru/kuhtich) <br/>
Антифрод: [Евгений Головенков](https://staff.yandex-team.ru/golovenkov)


### Желательное время исправления в случае поломки

В день обнаружения.


### Способы регулирования работы джобы

- Через проперти `FRAUD_PROMO_REDIRECTS_LAST_ROW` можно попробовать перечитать часть таблицы - например, если проскипали из-за бага и не дернули Баланс.


### Известные причины поломок

В пределах допуска мониторинга не ломалась. Предположительно, таблица может перестать быть append-only или вообще потеряться. Может рваться соединение с YT, может непредсказуемо отвечать Баланс.


### Дополнительно: тонкости и подводные камни
