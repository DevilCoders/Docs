# Датасет аудитории мобильного приложения Я.Карт (сэмплированный)
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/users-days/mobile-maps/all)

- [Датасет в Datalens TBD]()

## Примеры расчетов по датасету

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/YDC49NK3DP9VRHF_hHmqswrJvizWgL1COBXnYPw2E6k=&#41; общее кол-во открытий, открытия с deep use, открытия геопродукта;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQcJ3udkiRg5LGzENueRmFhNsTZDImMBrX8T2-MNQ=&#41; открытия по зумам;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQeBpqv-RDuss6eiYfPKuJk5iP2UorejVKF8aoAgQ=&#41; открытия по классу рубрик;)

## Отчеты и дашборды по датасету

[comment]: <> (* [Отчет]&#40;https://stat-beta.yandex-team.ru/Multiproject/datasets/basemap&#41; c метриками подложки;)


## Назначение

Каждая строка это уникальный кортеж ```(DeviceID, EventDate)```. Каждая строка это один пользователь, который пользовался сервисом в этот день и его характеристики.
Данные сэмплированы! В поле ```sampling_rate``` содержится число, на которое нужно домножать, чтобы получить оценку 100% данных.

## Для каких сервисов считается
* Мобильные карты

## Источники

cooked-логи мобильных карт  [cooked-metrika-mobile-log/mobile-maps](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log/mobile-maps)

Информация о первой установки приложения на девайс  [statadhoc-9770-metrika-mobile-apps-install-last](//home/maps/analytics/legacy/nile/statadhoc-9770-metrika-mobile-apps-install-last/)

## Схема расчета

Группируем cooked логи по DeviceID и EventDate. Для каждой пары считаем метрики. Приджойниваем дату установки из ```metrika-mobile-apps-install```
## Модель данных и описание полей
Таблица обновляется ежедневно

**Описание полей**

|  | Поле | Физический смысл |
|:------------- |:-------------| -------------|
| 1| EventDate | Дата |
| 2|  DeviceID |DeviceID пользователя |
| 3|  AppPlatform | Android/iOS|
| 4|  AccountID |  паспортный ID |
| 5|  Age | Возраст из крипты |
| 6|  AppVersionName | Версия приложения |
| 7| RegionID |Регион из метрики |
| 8|  country | Название страны пользователя |
| 9|  district | Название округа пользователя |
| 10|  region | Название региона пользователя |
| 11|  city | Название города пользователя |
| 12|  install_date |  Дата первой установки на телефон |
| 13|  sampling_rate |  число, на которое нужно домножать, чтобы получить оценку 100% данных |

## К кому можно обращаться с вопросами

Вопросы задавать можно timnosov@, ikolodkin@.
