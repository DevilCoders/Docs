# Ежечасовая выгрузка bigB профилей пользователей, информацию о которых запрашивала БК
- [Путь на YT](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/geodisplay/analytics/regular/bigb_crypta_profiles/1h)

## Отчеты и дашборды по датасету

На момент обновления README.md нет дашбордов

## Источники
[хит логи bigB](https://yt.yandex-team.ru/hahn/navigation?path=//logs/maps-ads-geosearch-profile-hit-log/1h)

## Схема расчета
По данным из хит логов bigB парсим протобуф пользователя и складываем в таблицу bigb_crypta_profiles

## Модель данных и описание полей

| Поле                | Описание                                                                                                                                                                                                                                                           |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| device_id           | аппметричный id устройства                                                                                                                                                                                                                                         |
| log_timestamp       | Время получения логи                                                                                                                                                                                                                                               |
| timezone       | Часовой пояс, в котором указано время получения лога                                                                                                                                                                                                               |
| longterm_interests  | лист из segment_id долгосрочных интересов крипты. [Таблица](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/profiles/export/lab/segments) соответствия названия интереса и segment_id. Нужно фильтровать таблицу по exportKeywordId = 601  |
| shortterm_interests | лист из segment_id краткосрочных интересов крипты. [Таблица](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/profiles/export/lab/segments) соответствия названия интереса и segment_id. Нужно фильтровать таблицу по exportKeywordId = 602 |
| heuristic_common    | лист из segment_id эврестических интересов крипты. [Таблица](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/profiles/export/lab/segments) соответствия названия интереса и segment_id. Нужно фильтровать таблицу по exportKeywordId = 547 |
| audience_segments   | лист из segment_id сегментов аудиторий крипты. [Таблица](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/profiles/export/lab/segments) соответствия названия интереса и segment_id. Нужно фильтровать таблицу по exportKeywordId = 557     |
| gender              | m, f, null                                                                                                                                                                                                                                                         |
| age_segment         | возраст (6 сегментов). Подробнее можно почитать на wiki-страничке крипты                                                                                                                                                                                           |
| income_segment      | A, B, C. Подробнее можно почитать на wiki-страничке крипты                                                                                                                                                                                                         |
| income_5_segment    | A, B1, B2, C1, C2. Подробнее можно почитать на wiki-страничке крипты                                                                                                                                                                                               |

## К кому можно обращаться с вопросами

Вопросы можно задавать aladgou@.
