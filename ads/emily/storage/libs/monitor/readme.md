# Emily Monitor

Библиотека для отправки метрик в соломон в проект Emily.

## Как использовать

1. Реализовать необходимые мониторы

    ```py
    from ads.emily.storage.libs.monitor.lib.monitor import BaseMonitor
    from ads.emily.storage.libs.monitor.lib.metric import ModelMetric

    class NewMonitor(BaseMonitor):
        def __init__(self, client):
            pass

        def get_metrics(
                self,           # type: BaseMonitor
                relative_time,  # type: datetime
        ):  # type: (...) -> tp.List[BaseMetric]
            ...
            return [
                ModelMetric(
                    sensor="sensor_name",
                    value=12.21,
                    key="model_key",
                    labels={}  # custom labels
                    time=datetime.now()  # optional metric time
                ),
            ]
    ```

2. Отправить метрики через `EmilyMonitor`

    ```py
    from ads.emily.storage.libs.monitor import EmilyMonitor, EmilySolomon
    from ads.emily.storage.libs.monitor.lib.services import Services

    monitor = EmilyMonitor(
        solomon=EmilySolomon(token=<SOLOMON_TOKEN>),    # solomon client
        service=Services.SERVICE_NAME,                  # solomon service
    )

    # Вычислить метрики
    metrics = NewMonitor.get_metrics()

    # Отправить метрики в кластер Соломона
    monitor.push(metrics)
    ```
