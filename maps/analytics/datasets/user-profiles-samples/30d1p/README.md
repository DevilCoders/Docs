# Ежемесячная выгрузка сэмпла (1%) профилей крипты аудитории геосервисов
- [Путь на YT](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/datasets/user-profiles-samples/30d1p)

## Отчеты и дашборды по датасету

- [Дашборд MAU геосервисов с аудиторией крипты](https://datalens.yandex-team.ru/opxzibpkk42cg-crypta-segments?state=8bb3ab6c403)

## Источники
[DAU геосервисов с профилями крипты](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/user-profiles)

## Схема расчета
Объединяю ежедневные таблицы за 30 дней, оставляю самые свежие профили крипты для каждого уникального пользователя, объединяю данные 3 сервисов (mobile-maps, mobile-metro, navi), сэмплирую данные (1%), вертикально раскрываю список с интересами и получаю строки, уникальные по пользователю, сервису и интересу. Подробнее в коде

## Модель данных и описание полей

|Поле| Описание                                                   |
|----|------------------------------------------------------------|
| device_id| аппметричный id устройства                                 |
| service| navi, mobile-maps, mobile-metro                            |
| geo_id| RegionID пользователя                                      |
| gender| m, f, null                                                 |
| age_segment| возраст. Подробнее можно почитать на wiki-страничке крипты |
| income_segment| high, middle, low                                          |
| segment_name| Интерес или аудиторный сегмент пользователя                |

## К кому можно обращаться с вопросами

Вопросы можно задавать aladgou@, ikolodkin@.
