## Утилита для получения статусов операций из графов Nirvana

Используя Nirvana API получает статусы и зависимости операций из всех инстансов конкретного Workflow.
Как идентификатор операции используется параметр `mnclose_task`.

Возращает информацию об операциях в формате JSON:

```json
[
    {
        "code_id": 123,
        "task_id": "ar_import_private_deals", 
        "title": "Получить справочник частных сделок",
        "start_date": 1566209933,
        "start_deadline": 0,
        "finish_date": 1566210539,
        "finish_deadline": 0,
        "duration_limit": 0, 
        "status": "completed", 
        "result": "success", 
        "alert_state": "OK", 
        "alert_message": "",
        "offset": 0,
    },
    {
        // ...
    }
]
```

Также возвращает информацию о состояниях алетров в формате JSON:
```json
[
    {
        "service": "nirvana_monthclose_08_19_task_ar_import_private_deals",
        "status": "OK",
        "description:": "Task is OK"
    },
    {
        "service": "nirvana_monthclose_08_19_task_dcs_uao",
        "status": "CRIT",
        "description:": "Missed finish deadline"
    }
]
```

И информацию о зависимостях между операциями в формате JSON:
```json
[
    {
        "from": "get_stat_from_bk",
        "to": "cmp_partner_fee"
    },
    {
        "from": "get_stat_from_bk",
        "to": "enqueue_partner_acts"
    }
]
```

Даты возвращаются в виде Unix timestamp (часовой пояс UTC).

### Параметры

- `workflow-id=3e9a5af8-8920-44ac-bf51-bdf327866a52` – идентификатор Workflow, статусы операций в instance которого нужно вернуть.
- `nirvana-server=test.nirvana.yandex-team.ru` – какой сервер Nirvana использовать, продовый или тестовый.
- `alert-service-prefix=nrivana_monthclose_08_19_test_task_` – префикс сервиса в сырых событиях Juggler.
- `alert-rules-filename=./alert-rules.json` – путь к файлу с правилами, по которым вычисляются алерты. 

    Пример содержимого:
    ```json
    {
        "adfox_alignment": { // id задачи (должен соответствовать mnclose_task
            "start_deadline": 60 // Дедлайн начала задачи, в минутах от (начало месяца + offset) (т.е. тут - 01:00 первого дня)
        },
        "dcs_uao": {
            "finish_deadline": 600, // Дедлайн завершения задачи, в минутах от (начало месяца + offset) (т.е. тут - 10:00 второго дня)
            "duration_limit": 3600, // Лимит по времени выполнения задачи, в минутах
            "offset:" 1440 // Смещение от начала месяца, в минутах. От этого смещения отсчитываются алерты по дедлайнам.
                           // Используется для того чтобы сдвинуть выполнение ручных задач в месяцы, когда 1 число выпадает на выходной
        }
    }
    ```
- `token-filename=./token` – путь к файлу с OAuth токеном для Nirvana.
- `statuses-filename=./statuses.json` – путь к файлу, в который будет записана информация об операциях. Если опущено – информация будет выведена в лог.
- `alerts-filename=./alerts.json` – путь к файлу, в который будут записаны статусы алертов. Если опущено – статусы будут выведены в лог.
- `dependencies-filename=./dependencies.json` – путь к файлу, в который будут записаны зависимости между операциями.
- `month-start-tz-offset=10800` – смещение часового пояса, в котором отсчитывается начало процесса закрытия месяца (00:00 1го числа). В секундах. Для Москвы – 3 часа = 10800.
