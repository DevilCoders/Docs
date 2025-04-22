# Ежедневная выгрузка криптопрофилей пользователей //home/maps/analytics/datasets/user-profiles/
- [Путь на YT](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/datasets/user-profiles)

## Отчеты и дашборды по датасету

## Источники
[appmetrica-yandex-events](https://yt.yandex-team.ru/hahn/navigation?path=//logs/appmetrica-yandex-events/1d)

[криптопрофили crypta_id](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/profiles/export/cryptaid)

[дневные таблицы плюса](https://yt.yandex-team.ru/hahn/navigation?path=//home/msdata/dwh/cdm/plus_user/daily)
## Схема расчета
Склеиваем криптопрофили и DAU МЯКа, Нави и Метро по device_id, по puid добавляем информацию о том, в плюсе ли пользователь

## Модель данных и описание полей

|Поле| Описание                                                                                                                                                                                                                                                           |
|----|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| uuid| id установки                                                                                                                                                                                                                                                       |
| crypta_id| id крипты                                                                                                                                                                                                                                                          |
| puid|                                                                                                                                                                                                                                                                    |
| device_id| аппметричный id устройства                                                                                                                                                                                                                                         |
| service| navi, mobile-maps, mobile-metro                                                                                                                                                                                                                                    |
| os| android, iOS, WindowsPhone                                                                                                                                                                                                                                         |
| geo_id| География пользователя                                                                                                                                                                                                                                             |
| longterm_interests| лист из segment_id долгосрочных интересов крипты. [Таблица](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/profiles/export/lab/segments) соответствия названия интереса и segment_id. Нужно фильтровать таблицу по exportKeywordId = 601  |
|shortterm_interests| лист из segment_id краткосрочных интересов крипты                                                                                                                                                                                                                  |
| heuristic_common| лист из segment_id эврестических интересов крипты. [Таблица](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/profiles/export/lab/segments) соответствия названия интереса и segment_id. Нужно фильтровать таблицу по exportKeywordId = 547 |
| audience_segments| лист из segment_id сегментов аудиторий крипты. [Таблица](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/profiles/export/lab/segments) соответствия названия интереса и segment_id. Нужно фильтровать таблицу по exportKeywordId = 557     |
|prism_cluster| Призма. Подробнее в [wiki](https://wiki.yandex-team.ru/jandekspoisk/prism/)                                                                                                                                                                                        |
| gender| m, f, null                                                                                                                                                                                                                                                         |
| age_segment| возраст (6 сегментов). Подробнее можно почитать на wiki-страничке крипты                                                                                                                                                                                           |
| income_segment| A, B, C. Подробнее можно почитать на wiki-страничке крипты                                                                                                                                                                                                         |
| income_5_segment| A, B1, B2, C1, C2. Подробнее можно почитать на wiki-страничке крипты                                                                                                                                                                                               |
| plus_tariff_bundle_id | id подписки плюса |

## К кому можно обращаться с вопросами

Вопросы можно задавать aladgou@.
