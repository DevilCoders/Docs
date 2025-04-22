# Админка персональных целей

## Работа с персональными целями
### Загрузка целей
Загрузка целей должна работать так:
в форму загрузки цели вставляется адрес YT-таблицы определенного формата.  
Ручка будет закрыта драфтом, см. [PR в сервис драфтов](https://github.yandex-team.ru/taxi/backend-py3/pull/8067)   
После подтверждения драфта запускается STQ-таска `personal_goals_upload`, которая выгружает цели из YT и загружает их в postgres.

![](https://wf.yandex-team.ru/plantuml/fLRBRjf05DtxAqPUDye-Yogg8dNHHLg5JLPeW0crQcpN7jAYgb82JL6Kgb5MtVGZ20s5aW2_CFD7FVVQ1fiW1RMHmcEuZtFFENV0sK-qZ7MxvJkohiDOkEQd6PaP_k_CRpEoPwwGYMZ9G3PLx3WHWhsw5yb02_SWbYSw4KSgFlNgYWCRV5GEUwtY90oaBrw6qY-7Hyrow57b3Pyd-htJa5hMPA8U5JXuaRQg5KAEAtpMqOwJOHKxppCqUyAUcxaPOwA1xTflmjpPCxpyOhjE6a6nKNDFkExhmwEAsFK2hM8qt9MDbXVidahVGojLhRNzTzLsv8UouRfErEGUDTJlsowpDZ4ZWOSnAYNALtNjXK6Ma20Z2BKIiTTygns1FxC0ZhaP4ircQWR0QIzGvy5UYUFA3ceEpAsvDnFxrLuvAcW8Ak0qQYkyXwzMGB9XiqFkvQiJJV2umunxJSoqm8UP5IWeqNMBjc09cLs1jrCpmHEzVYZxWufkufo7csJHatNU2-YoucbJRZd3j5i9mzvTKwKW2qOSc0MQdrFpuMPHHDuxuoFLS65xoEhQAtkHo_GBZoCSKknmSxbg58VDM2M9ei8KIP9ssNOzJdn0LWGblQ1PyeF83C6CWjiITljTuFpItWYcPrmoZhqcYH1s_Onhi1VdXNoK-mCOWkqq9Ka4AIUMui1mZ-sM0SAdD4BFNlBiNJEqFUhtf1knmH3W1u7WqQUfbGWd8w4ZvY9TxMeJgrrTvtE3jp-v45st4nTlP1Jv7MBoCmBzC8o8m3bl4WF7gpdCr6V-gJ7GNs74EQ_RX3Gi3esCuue3u4l_e5gg7-rDQk5YXL59NO3pWgK3o5XFMcGhq0IC00fsNR5zZhMZSw-JBO048PJTfoibpOO7d8vU2PC553yk3bvQd4t5Q6jWe9cPib_PIBWSNDUNYQx6uOUg5pJKHum8e_mNf_Mm5VbAg-q8pJgbG-RRj01ctkniQ_8jptre1enoJGtQ72GGolF2rPLkFoj5aVU0sQT1rhovX4tU_EVBh72NRVYkM5qiWrGoN55Opt5kxgV8AgvkoRhRRntnjfek_vbGlDsNn9M-4UmDlddsaKs_F9o_)

#### STQ-таск
Для загрузки будет создана новая stq-очередь `personal_goals_selection_upload`.

Для отслеживания прогресса загрузки будет создана ещё одна таблица:
```sql 
create table selection_upload_progresses
(
    selection_id   text references selections,
    yt_table_name  text        not null,
    last_row_index integer     not null,
    status         text        not null -- принимает значения (pending, in_progress, complete),

    created        timestamptz not null default now(),
    updated        timestamptz not null default now()
)
```

При вызове ручки валидации проверяется, что схема YT-таблицы соответствует ожидаемой.
После подтверждения драфта вызывается ручка загрузки.
При первом запуске для каждого selection id из таблицы ручка загрузки создаёт selection_upload_progress.
После этого ручка запускает таск загрузки с id равным имени таблицы в YT.

У каждой строчки в YT-таблице есть номер. Его мы будем записывать в `last_row_index`.
STQ-таск начинает загружать цели чанками и увеличивать `last_row_index`, пока не дойдёт до конца выборки.
При записи цели проверяется, что у пользователя нет целей с данным брендом, которые пересекаются по времени выполнения. Это позволит загружать цели заранее. 
Если проверка не выполняется, цель пропускается, id цели возвращается сервису драфтов в сообщении со статусом `partially_completed`.
Если таска прерывается и запускается заново, она смотрит на значение `last_row_index` и соответствующее значение selection_id и продолжает загружать эту выборку.
Когда выборка кончается, STQ-таск ставит статус загрузки в `complete` и перепланирует себя с тем же id. 

Сервис драфтов периодически ходит в ручку загрузки. Ручка загрузки проверяет статус прогрессов, связанных с именем YT-таблицы и отвечает `in_progress`, если загрузка ещё идет или `complete`, когда загрузка закончилась.


#### Формат YT таблицы

| selection_id  | goal_id | yandex_uid | conditions                              | bonus                 | application |
|---------------|---------|------------|-----------------------------------------|-----------------------|-------------|
| new_year_goal | goal_1  | 999999     | {'type': 'ride', 'classes': ['econom']} | {'type': 'promocode'} | yandex      |
| new_year_goal | goal_2  | 123456     | {'type': 'ride', 'classes': ['econom']} | {'type': 'promocode'} | yandex      |
| new_year_goal | goal_3  | 7183472    | {'type': 'ride', 'classes': ['econom']} | {'type': 'promocode'} | yandex      |
### Активация целей 

#### Ручка активации цели
Активация целей будет работать через существующую ручку `/internal/admin/selections/update`.  
В неё нужно будет передать `selection_id`, с которым были загружены цели и `status` со значением `active`

### Скрытие пользовательских целей
через ручку /internal/admin/selections/update, принимающую на вход 
selection_id, в поле `status` необходимо передать `hidden`


## Этапы
1. Раскатка персональных целей
    1. Загрузка целей
        - миграция: добавить таблицу прогресса загрузки `selection_upload_progresses`
        - ручка валидации драфта `/internal/admin/validate_goals_upload_from_yt`
            - проверять формат YT-таблицы
            - проверять, что загрузка выборок из YT-таблицы ещё не началась 
        - ручка применения драфта `/internal/admin/upload_goals_from_yt`
            - создавать запись в таблице загрузок
            - запускать stq-таск
            - возвращать статус загрузки
        - stq-таск для загрузки выборки `personal_goals_selection_upload`
            - по батчам загружать цели из YT в базу
            - проверять время действия цели при загрузке
            - перепланировать себя после записи каждой выборки 
        - добавить фильтр на время действия во всех ручках получения целей
    2. Генерация промокодов
        - TBD
