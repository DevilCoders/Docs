# Данный о установленных приложениях (пока только ios)
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/apps-installs)


## Отчеты и дашборды по датасету

Инсталлы 2gis и карт  на ios по событиям отправленным приложением такси

https://datalens.yandex-team.ru/js1p89xuo960c-maps-and-2gis-ios-app-installs
## Назначение

* Хранит ежедневные данные об установках приложений (пока только на ios устройствах)

* Хранит еженедельные данные об установках 2гис и карт по данным отправленными такси в разбивке по ФО  (только на ios устройствах)

## Для каких сервисов считается

*  Навигатор
* Мобильные карты


## Источники

Логи аппметрики [appmetrica-yandex-events](https://yt.yandex-team.ru/hahn/navigation?path=//logs/appmetrica-events-log/appmetrica-yandex-events)
Логи аппметрики такси [taxi-metrika-mobile-log](https://yt.yandex-team.ru/hahn/navigation?path=//logs/appmetrica-events-log/taxi-metrika-mobile-log)

## Схема расчета

Для таблицы ios/1d: [YQL запрос](https://a.yandex-team.ru/arc_vcs/maps/analytics/data/apps-installs/ios/1d/query.sql) входной параметр date = дата

Для таблицы ios/1w-maps: [YQL запрос](https://a.yandex-team.ru/arc_vcs/maps/analytics/data/apps-installs/ios/1w-maps-vs-dgis-from-taxi/query.sql) входной параметр date = дата понедельника расчитываемой недели

## Модель данных и описание полей

Таблица ios/1d содержит дневные данные об установках приложений и приложениях-источниках логов об этом

**Описание полей**

|  | Поле | Физический смысл |
|:------------- |:-------------| -------------|
| 1| user_id | DeviceID из appmetrica|
| 2|  APIKey | APIKey приложения передавшего логи |
| 3|  DeviceType | DeviceType из appmetrica Тип устройства: 0/UNKNOWN - не определён, 1/PHONE - телефон, 2/TABLET - планшет, 3/PHABLET - фаблет (не используется с версии 2.0 Android SDK), 4/TV - телевизор, 5/DESKTOP - десктоп|
| 4|  Model | Модель устройства |
| 5|  app_name | Имя установленного приложения |
| 6|  region | ID региона устройства|

**Описание полей**
Таблица ios/1w-maps содержит агрегированые данные по географии оценки использования карт и 2gis

|  | Поле | Физический смысл |
|:------------- |:-------------| -------------|
| 1| week | Дата |
| 2| district | Географический район |
| 3| app_name | Имя приложения |
| 4| app_installs | Количество установок |
| 5| audience | Объем аудитории |
| 6| frac | Доля приложения относительно аудитории |

## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики в [Slack](https://join.slack.com/share/zt-jfgq9obr-8WV8gxokWri3A1wa9TrBjg?cdn_fallback=1) или andrey-shan@.

