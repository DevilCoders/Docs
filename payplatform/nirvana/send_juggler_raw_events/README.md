## Утилита для отправки сырых событий в Juggler.

Отправляет сырые события в Juggler, как описано здесь: https://wiki.yandex-team.ru/sm/juggler/batching/.

На вход принимает информацию о состояниях алетров в формате JSON:
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

### Параметры

- `--juggler-url=http://juggler-push.search.yandex.net/events` – адрес ручки, в которую пушить сырые события.
- `--host=nirvana_send_juggler_raw_events` – имя хоста события (см. документацию на вики, ссылка выше).
- `--source=nirvana_send_juggler_raw_events` – источник события (см. документацию на вики, ссылка выше).
- `--raw-events-filename=./alerts.json` – путь к файлу с описанием состояния алертов. 
- `--batch-size=75` – (необязательный параметр) размер батча сырых событий. На вики рекомендуют не больше 100, т.к. есть ограничение на размер тела запроса. 
- `--tag=some-application-specific-tag` – (необязательный параметр) тэг сырого события, по которому их можно потом найти.