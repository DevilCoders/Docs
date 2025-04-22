# Датасет инсталлов МЯК в разрезе опций (тач-дистрибуция)

- [Таблица на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/reports/marketing/touch-distribution/banners)

## Отчеты и дашборды по датасету

- [Ссылка на сам дашборд](https://datalens.yandex-team.ru/rhdesdz7nihyj-performance-geoservices?tab=g6)
- [Datalens dataset](https://datalens.yandex-team.ru/datasets/1gpyz60uv182v-interstitial-installs)

## Назначение

Хранит исторические данные по количеству показов/кликов баннеров в разрезе опций и браузеров. Сейчас актуальные данные подтягиваются из Директа (раньше была Banana).

## Источники

Данные по баннерам из Директа [bs-chevent-cooked-log](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//statbox/cooked_logs/bs-chevent-cooked-log/v2/1d)

## Схема расчета

Таблица пересобирается с последнего понедельника предыдущего месяца до вчерашнего дня, обновляются только те недельные/месячные агрегации, которые затрагиваются в эту дату.

## Модель данных и описание полей
Таблица обновляется ежедневно.

**Описание полей**

|  | Поле | Физический смысл |
|:------------- |:-------------| -------------|
| 1|  browser_name | Браузер пользователя|
| 2|  event_date | Дата показа/клика |
| 3|  period | Временная агрегация ('Daily' / 'Weekly' / 'Monthly')|
| 4|  order_id | Идентификатор баннера |
| 5|  context_option | Название опции баннеров |
| 6|  shows | Количество показов баннеров |
| 7|  clicks_total | Суммарное количество кликов по баннерам|
| 8|  clicks_close | Количество кликов по крестику на баннерах |
| 9|  clicks | Количество кликов по баннерам|

## К кому можно обращаться с вопросами

Вопросы задавать можно dianamir@ .
