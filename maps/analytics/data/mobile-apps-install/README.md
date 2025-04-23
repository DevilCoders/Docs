# Датасет пользователей и дата установки приложения
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/mobile-apps-install/mobile-maps)

- [Датасет в Datalens TBD]()

## Примеры расчетов по датасету

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/YDC49NK3DP9VRHF_hHmqswrJvizWgL1COBXnYPw2E6k=&#41; общее кол-во открытий, открытия с deep use, открытия геопродукта;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQcJ3udkiRg5LGzENueRmFhNsTZDImMBrX8T2-MNQ=&#41; открытия по зумам;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQeBpqv-RDuss6eiYfPKuJk5iP2UorejVKF8aoAgQ=&#41; открытия по классу рубрик;)

## Отчеты и дашборды по датасету

[comment]: <> (* [Отчет]&#40;https://stat-beta.yandex-team.ru/Multiproject/datasets/basemap&#41; c метриками подложки;)


## Назначение

Каждая таблица содержит всех пользователей за все время (с 2015 года). Каждая строка это уникальный кортеж ```(DeviceID)```. Каждая строка это один DeviceID и дата установки приложения.


## Для каких сервисов считается
* Мобильные карты

## Источники

cooked-логи мобильных карт  [cooked-metrika-mobile-log/mobile-maps](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log/mobile-maps)

## Схема расчета

Берем исторические данные и берем новые установки за сегодня. Объединяем их и оставляем дату самой первой установки на девайс.

>## Модель данных и описание полей
Таблица обновляется ежедневно

**Описание полей**

|  | Поле | Физический смысл |
|:------------- |:-------------| -------------|
| 1| DeviceID | DeviceID |
| 2|  install_date |Дата первой установки |
## К кому можно обращаться с вопросами

Вопросы задавать можно timnosov@, ikolodkin@.
