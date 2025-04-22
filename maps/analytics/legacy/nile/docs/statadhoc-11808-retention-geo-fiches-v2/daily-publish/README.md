| | |
|:------------- |:-------------:|
| Результат | Отчет [Ретеншн в фичу (Ежедневный)](https://stat.yandex-team.ru/Multiproject/Adhoc/retention-geo-fiches_v2_daily) |
| Сервисы | моб карты, нави |
| Описание | Считается по [словарю](https://a.yandex-team.ru/arc/trunk/arcadia/statbox/jam/configs/geo-analytics/feature_retention_report_ver2.yaml). Для дней - лаг 7 дней, Используется rolling retention для недель - лаг 5 недель, Используется классический retention. Пример использования отчета: 1) выбираем фичу (напр. search) 2) ставим дневной скейл 3) выбираем дельта = 2 4) Тогда показатель retention для дня Х будет означать долю пользователей, которые воспользовались этой фичей в день Х и потом в один из дней [X+2, X+7], от общей аудитории фичи в день Х |
| Первый тикет | [STATADHOC-11808](https://st.yandex-team.ru/STATADHOC-11808) |
| Добавление в Буддату | [MAPSINFRA-900](https://st.yandex-team.ru/MAPSINFRA-900)
