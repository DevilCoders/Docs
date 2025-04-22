# Данные о подключенных картах лояльности пользователей Заправко
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/zapravki-bonus-card)

[comment]: <> (- [Датасет в Datalens]&#40;https://datalens.yandex-team.ru/datasets/gbb5tdzdmn3gc-basemap&#41;)

## Примеры расчетов по датасету

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/YDC49NK3DP9VRHF_hHmqswrJvizWgL1COBXnYPw2E6k=&#41; общее кол-во открытий, открытия с deep use, открытия геопродукта;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQcJ3udkiRg5LGzENueRmFhNsTZDImMBrX8T2-MNQ=&#41; открытия по зумам;)

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/XwxQeBpqv-RDuss6eiYfPKuJk5iP2UorejVKF8aoAgQ=&#41; открытия по классу рубрик;)

## Отчеты и дашборды по датасету

[comment]: <> (* [Отчет]&#40;https://stat-beta.yandex-team.ru/Multiproject/datasets/basemap&#41; c метриками подложки;)


## Назначение

* Хранит данные о подключенных картах лояльности в Яндекс Заправках

Одна строка таблицы соответствует паре пользователь - программа лояльности


## Источники



Данные бэкенда Заправок [dictionary user](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/zapravki/production/replica/transfer-manager/mongo/dictionary_user)


## Модель данных и описание полей
Таблица обновляется раз в день

**Описание полей**

|  | Поле | Физический смысл |
|:------------- |:-------------| -------------|
| 1| add_datetime |Дата и время первого добавления карты|
| 2|  card_id |Название программы лояльности|
| 3|  puid | Паспортный идентификатор пользователя|

## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики в [Slack](https://join.slack.com/share/zt-jfgq9obr-8WV8gxokWri3A1wa9TrBjg?cdn_fallback=1).

