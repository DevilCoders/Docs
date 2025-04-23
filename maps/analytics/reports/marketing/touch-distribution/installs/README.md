# Датасет инсталлов МЯК в разрезе опций (тач-дистрибуция)

- [Таблица на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/reports/marketing/touch-distribution/installs)

## Отчеты и дашборды по датасету

- [Ссылка на сам дашборд](https://datalens.yandex-team.ru/a9tdtbo8g8x46-performance-geoservices?tab=g6)
- [Datalens dataset](https://datalens.yandex-team.ru/datasets/1gpyz60uv182v-interstitial-installs)

## Назначение

Хранит исторические данные по количеству инсталлов в разрезе опций, платформ и географии.

## Источники

Данные мобильной метрики об инсталлах [metrika-mobile-install-log](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//logs/metrika-mobile-install-log/1d)

## Схема расчета

Берутся исторические данные о скачивании приложения Яндекс Карт за весь пеирод с 2021-01-01 числа по вчерашний день.

## Модель данных и описание полей
Таблица обновляется ежедневно.

**Описание полей**

|  | Поле | Физический смысл |
|:------------- |:-------------| -------------|
| 1| app_platform | Платформа устройства |
| 2|  browser_name | Браузер пользователя|
| 3| geo | География (либо 'Russia', либо 'World')|
| 4|  install_date | Дата инсталла приложения|
| 5|  period | Временная агрегация ('Daily' / 'Weekly' / 'Monthly')|
| 6|  type | Глобальный тип инсталла ('Fullscreen' / 'Interstitial' / 'Routes-guidance' / 'Smart-banner' / 'Nativ-menu' / 'Others')|
| 7|  type_detailed | Детализированный тип инсталла|
| 8|  users | Количество уникальных DeviceIDHash с таким типом инсталла|

## К кому можно обращаться с вопросами

Вопросы задавать можно dianamir@ .
