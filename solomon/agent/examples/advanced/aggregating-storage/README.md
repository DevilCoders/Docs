## Предагрегация на стороне Агента

1. Fetcher забирает данные Агента в pull режиме (шард `(project=my_project; service=my_service)`, значение **cluster** выставляется на бэкенде)
2. Агент получает данные из HTTP запроса (push)
3. Агент агрегирует данные и после этого пишет их в хранилище. Интервал агрегации указан в agent.conf -> Storage -> AggregationOptions

Запуск Агената:
```bash
$ solomon-agent --config ./agent.conf
```

Заливка данных в Агент и проверка получившихся значений:
```bash
$ curl -H "Content-Type: application/json" -d@metrics.json -g "http://[::1]:10050/"
$ curl -g "http://[::1]:9666/storage/read?project=my_project&service=my_service&pretty=true"
```

Более частые запросы
```bash
$ for i in `seq 10`; do curl -H "Content-Type: application/json" -d@metrics.json -g "http://[::1]:10050/" ; done
$ curl -g "http://[::1]:9666/storage/read?project=my_project&service=my_service&pretty=true"
```

## Важно!
Сейчас агрегация поддерживается только для сенсоров типа **GAUGE** и **IGAUGE**. Причина описана в [SOLOMON-3486](https://st.yandex-team.ru/SOLOMON-3486#5c9a0fb1aeebac001ffb2484)
