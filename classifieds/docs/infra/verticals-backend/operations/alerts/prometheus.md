# Генерация prometheus алертов

## Рулы

### prometheus_alert

```python
prometheus_alert(
  name = "alive", # имя таргета для базеля
  alert_name = "ServiceAlive", # Имя алерта в прометеусе
  expression = """up{_service="my-service"} > 4""",
  for_duration = "5m",
  host = "my-service", # имя хоста для juggler'а
  summary = "", # Краткое описание метрики
  description = "", # Подробное описание проверки.
  # Можно использовать плейсхолдер {{ $value }} для получение текущего значения метрики
  # или {{ $labels.<label>}} для получения label сработавшей метрики
  # https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/#templating
  tags = ["my-super-group"], # теги будут проброшены в juggler, если есть тег manual, то алерт будет проигнорен автоматикой.
  prod = True, # Генерировать алерт для продакшена
  test = False, # Генерировать алерт для тестинга
)
```

По умолчанию все проверки создаются и для прода, и для тестинга. Если для тестинга они не нужны, используйте `test = Falsе`.

## Примеры
Примеры можно найти в [репозитории](https://a.yandex-team.ru/arc_vcs/classifieds/verticals-backend/common/alerts).

## Автоматизация
В [апстрим][1] попадают только алерты перечисленные в [//tools/prometheus:alerts](https://a.yandex-team.ru/arc_vcs/classifieds/verticals-backend/tools/prometheus/BUILD).
По умолчанию там перечислены все алерты, у которых не стоит тег `manual`.
Чтобы обновить этот список нужно запустить команду `make alerts`.
После того как измененные алерты попадают в мастер, автоматически создается PR в апстриме.

[1]: https://a.yandex-team.ru/arc_vcs/classifieds/prometheus-config
