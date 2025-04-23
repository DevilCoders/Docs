__Структура__

```
walkin
    |candidates   - кандидаты на walkin. Дневные таблицы. [Lifetime - 30 дней] 
    |profile      - профили пользователей
        |graph    -  маппинги id
            |user_uuid
                |user_id
                |yandex_uid
                |appmetrika_id
            |crypta_id
                |user_uuid 
        |socdem       - экспрт  из крипты с соцдемом пользователей
        |offers       - объявления, созданные пользователями на авто.ру
    |import
        |dealers      - экспорт из вербы со всеми автодилерами
    |export
        |all_orgvisit - оргвизиты по всем 
        |walkin       - плоская таблица со всеми walkin-ами
        |walkin_ydb-raw_json
        |walkin_ydb-agg
        |metrics      - метрики для дашборда по процеессу построения walkin-ов
        |walkin_share_metrics - метрики для дашборда про долю walkin-ов
```