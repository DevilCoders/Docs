# Датасет заявок и контрактов корпоративных клиентов Яндекс.Заправок
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/zapravki-corp-contracts)

- [Датасет в Datalens]()

## Примеры расчетов по датасету

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/YDC49NK3DP9VRHF_hHmqswrJvizWgL1COBXnYPw2E6k=&#41; общее кол-во открытий, открытия с deep use, открытия геопродукта;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQcJ3udkiRg5LGzENueRmFhNsTZDImMBrX8T2-MNQ=&#41; открытия по зумам;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQeBpqv-RDuss6eiYfPKuJk5iP2UorejVKF8aoAgQ=&#41; открытия по классу рубрик;)

## Отчеты и дашборды по датасету

[comment]: <> (* [Отчет]&#40;https://stat-beta.yandex-team.ru/Multiproject/datasets/basemap&#41; c метриками подложки;)


## Назначение

Хранит данные о заявке коропоративного клиента, а так же о контракте и водителях в случае если контракт был заключен.

В таблице содержатся все заявки корп. клиентов - и те, по которым заключили контракт, и те по которым не заключали.

[comment]: <> (## Для каких сервисов считается)

## Источники
Реплика базы заявок корп.клиентов [dictionary_corporation](https://yt.yandex-team.ru/hahn/navigation?path=//home/zapravki/production/replica/transfer-manager/mongo/dictionary_corporation);
Реплика базы логинов и email корп.клиентов для доступа в личный кабинет [tanker_authorize](https://yt.yandex-team.ru/hahn/navigation?path=//home/zapravki/production/replica/transfer-manager/mongo/tanker_authorize);

## Схема расчета
Выгружаем все заявки из базы заявок корп.клиентов ЯндексЗаправок. Джойним с данными о логинах, чтобы собрать все email
и телефоны. Если в заявках были указаны одинаковые email или телефоны, приписываем им одинаковый equality_id.

## Модель данных и описание полей
Таблица полностью пересчитывается ежедневно.

**Описание полей**

|  | Поле | Физический смысл |
|:------------- |:-------------| -------------|
| 1|    `users` | Пользователи личного кабинета |
| 2|    `account_settings` | Настройки аккаунта|
| 3|    `city` | Город (текстовое поле из заявки) |
| 4|    `company` | Json c информацией про компанию |
| 5|    `corp_id` | Id корп. клиента (заявки) |
| 6|    `create_timestamp` | Timestamp создания заявки, UTC |
| 7|    `date_create` | Дата создания заявки, iso-формат, московское время |
| 8|    `date_update` | Дата обновления заявки, iso-формат, московское время |
| 9|    `document_numbers` | Номера контрактов |
|10|    `emails` | Emails |
|11|    `equality_id` | Идентификатор дубля заявки |
|12|    `group` | Группа, к какой относится корп. клиент |
|13|    `integration_settings_provider` | Словарь (int) откуда пришла регистрация |
|14|    `taxi_billing_data` | Информация по договору и счёту на пополнения со счета Я.Такси ЛСТ (yson)|
|15|    `corp_billing_data` | Информация по договору и счёту на ручные пополнения (предоплатный счет) (yson) |
|16|    `corp_card_billing_data` | Информация по договору и счету по корп карте (636 сервис) (yson) |
|17|    `name` | Контактное лицо |
|18|    `phones` | Телефоны |
|19|    `self_registration` | Была ли регистрация самостоятельной |
|20|    `status` | Статус |
|21|    `update_timestamp` | Timestamp обновления заявки, UTC |
|22|    `has_contract` | Есть ли по заявке заключенный контракт |
|23|    `drivers_acivated` | Активированные водители |
|24|    `drivers_enable` | Доступные водители |
|25|    `drivers_remove` | Отключенные водители |
|26|    `drivers_all` | Все водители |
|27|    `integration_settings_domain` | Кастомная ссылка для регистрации кабинета |

## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики в [Slack](https://join.slack.com/share/zt-jfgq9obr-8WV8gxokWri3A1wa9TrBjg?cdn_fallback=1) или lincnitnastya@, alyasevenyuk@.
