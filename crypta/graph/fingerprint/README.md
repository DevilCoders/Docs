## Фингерпринт iOS

### Виды фингерпринта
- match/appmetrica
    - матчит апп-метрику c апп-метрикой
    - собирает fp-связки mm_device_id - mm_device_id
    - таска для запуска обновления суповой таблицы - ```crypta.graph.fingerprint.match.appmetrica.lib.UpdateSoupEdges```
- match/ssp
    - матчит ccп c апп-метрикой
    - собирает fp-связки ssp_user_id - mm_device_id
    - таска для запуска обновления суповой таблицы - ```crypta.graph.fingerprint.match.ssp.lib.UpdateSoupEdges```

### Ежедневный запуск в сандбокс
- Настройка шедулера: [spine](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/spine/__init__.py?rev=r8112027#L576).
- Пример таски: [UpdateSoupEdges](https://sandbox.yandex-team.ru/task/956790606/view).
### Релиз
- Релизная машина [ЦУМ](https://tsum.yandex-team.ru/pipe/projects/crypta/delivery-dashboard/crypta_graph_fingerprint)
    - Сандбокс ресурс для сбора фп-связок: [CRYPTA_FP_BASE_TASK](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/crypta/graph/fingerprint/__init__.py?rev=r7944050#L9)
    - Сандбокс ресурс для фп-метрик: [CRYPTA_BINARY_FINGERPRINT_BUNDLE](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/crypta/run_binary/bundles.py?rev=r7677371#L4).

### Запуск локально
Пример
```bash
./bin/crypta-fingerprint --date 2021-04-26 run --task crypta.graph.fingerprint.match.appmetrica.lib.UpdateSoupEdges
```

### Метрики
- Все метрики считаются [тут](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/metrics/fingerprint).
- Основной [дашборд](https://datalens.yandex-team.ru/uj0m556sqfoir-unifiedcryptastats?tab=QyZ).
