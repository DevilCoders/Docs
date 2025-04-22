## Настройки

Базовые настройки такие же, как у yhttp::client. Ниже приведены примеры настройки дополнительных параметров.

Сервис живет за балансером:
```yaml
nodes: [ https://push.yandex.ru ]
stats_period: 5 # размер скользящего окна статистики для бюджета ретраев, в секундах
retry_policy:
    max_attempts: 3 # максимальное количество попыток на запрос
    codes: [500, 502, 503, 504] # список HTTP кодов, которые нужно ретраить
    budget:
        value: 0.2 # 20% допустимо ретраев в общей массе запросов
    backoff:
        base: 500ms # стартовая задержка между ретраями
        max: 2s # максимальная задержка между ретраями
        multiplier: 2 # множитель задержки по итерациям
```

Схема с дополнительным fallback-ом:
```yaml
nodes: [ https://blackbox-mail.yandex.net, https://blackbox.yandex.net ]
select_strategy: linear # первый запрос направляется в primary, ретрай - в fallback
stats_period: 5
retry_policy:
    max_attempts: 2
    codes: [500, 502, 503, 504]
    budget:
        value: 0.2
    backoff:
        base: 500ms
        max: 2s
        multiplier: 2
```

Схема с балансировкой на стороне клиента:
```yaml
nodes: [ https://node1, https://node2, https://node3 ]
select_strategy: weighted_random # нагрузка распределяется по нодам взвешенным рандомом
stats_period: 15 # размер скользящего окна статистики для бюджета ретраев и WRS
wrs:
    factor: 2 # чем больше factor, тем агрессивнее троттлятся сбоящие сервера
    ignore_last_failed: true  # не ретраить два раза подряд в один и тот же хост
retry_policy:
    max_attempts: 3
    codes: [500, 502, 503, 504]
    budget:
        value: 0.2
    backoff:
        base: 500ms
        max: 2s
        multiplier: 2
```

Рекомендации по настройке и более подробные описания находятся в соответствующих разделах документации.
