## MediascopePositionChangeProcessor

### Продукт/подсистема

Интеграция Директа с верификаторами рекламы.


### Роль в работе продукта/подсистемы

Отвечает за синхронизацию баннеров с пикселями Mediascope с их личным кабинетом.


### Датафлоу

- Процессор для ess, реагирует на изменения в баннерах и креативах.
- Формирует обновлённые данные.
- Отправляет их в апи Mediascope.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.MediascopePositionChangeProcessor.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'mediascopeintegration.MediascopePositionChangeProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Не основной сценарий, но тоже достаточно важная функциональность. Баннеры с пикселем Mediascope перестанут отправляться в их API, пострадает отображение статистики в личном кабинете Mediascope.


### Как пользователи (или команда) заметят проблему и через какое время

Новые баннеры перестанут появляться в кабинете Mediascope и к ним нельзя будет привязать показы.


### Контакты разработчиков и менеджеров

Разработчики: [Егор Иватько](https://staff.yandex-team.ru/ivatkoegor) <br/>
Менеджеры: [Алексей Александров](https://staff.yandex-team.ru/hrustyashko)


### Желательное время исправления в случае поломки

Главное выяснить на чьей стороне поломка - на нашей или на стороне Mediascope. Если на нашей, то чинить asap.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)
- Константа `POSITIONS_BATCH_SIZE` в [коде](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/service/MediascopePositionService.java) задает размер пачки данных, отправляемых в Mediascope.


### Известные причины поломок




### Дополнительно: тонкости и подводные камни
