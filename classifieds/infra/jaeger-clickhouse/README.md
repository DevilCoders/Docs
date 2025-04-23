# Jaeger ClickHouse

Хард-форк storage-плагина для ClickHouse с улучшениями:

- collector мимо grpc-плагина
- запись данных напрямую в шарды кликхауса
- фиксы со структурой данных и запросов к трейсам

Оригинал здесь: https://github.com/jaegertracing/jaeger-clickhouse

## Релиз

Запуск релизной сборки:

```bash
gh workflow run release -f docker_tag=SOME_TAG
```

## Эксплуатация:

- спеки в [nomad-jobs](https://github.com/YandexClassifieds/nomad-jobs)
- деплой через [jenkins](https://j.vertis.yandex-team.ru)
- Графики в [grafana](https://grafana.vertis.yandex-team.ru/goto/jaO3FB-7k?orgId=1)
