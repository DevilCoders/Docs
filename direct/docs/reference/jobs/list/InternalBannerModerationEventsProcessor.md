## InternalBannerModerationEventsProcessor

### Продукт/подсистема

[Внутренняя реклама (aka Банана)](../../../glossary/glossary.md#internal-ads).

### Роль в работе продукта/подсистемы

Баннеры внутренней рекламы могут быть автопринимаемыми или модерируемыми, это зависит от плейса (`place_id`). При сохранении баннера ему выставляется статус `banners.statusModerate == 'Yes' || 'Ready'`.

Данная джоба отправляет в Модерацию модерируемые баннеры Внутренней рекламы.


### Датафлоу

Классический модерационный ESS процессор.

- Отслеживает события в таблице [banners](https://direct-dev.yandex-team.ru/db/ppc/tables/banners.html) для баннеров указанного типа.
- Отправляет баннеры в Модерацию через LogBroker.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.InternalBannerModerationEventsProcessor.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'banner.InternalBannerModerationEventsProcessor)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Не будут отправляться в Модерацию модерируемые баннеры.


### Как пользователи (или команда) заметят проблему и через какое время

По статусу баннера увидят, что он долго находится в Модерации.

В рамках тикета [DIRECT-128950](https://st.yandex-team.ru/DIRECT-128950) возможно будет реализована отправка писем о застрявших баннерах.


### Контакты разработчиков и менеджеров

Разработчики: [Бехруз Афзали](https://staff.yandex-team.ru/xy6er), [Захар Зибаров](https://staff.yandex-team.ru/zakhar) <br/>
Менеджеры: [Ваня Пахомов](https://staff.yandex-team.ru/irpakhomov), [Марина Ежова](https://staff.yandex-team.ru/ezhova-m)


### Желательное время исправления в случае поломки

Как можно скорее.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Отсутствуют.
