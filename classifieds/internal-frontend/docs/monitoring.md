# Мониторинг

Для сбора метрик используем Prometheus. Выводим в Grafana.
RED метрики R(equest rate), E(error rate), and D(uration of requests) собираются в [мидлваре](https://github.com/YandexClassifieds/internal-frontend/blob/master/internal-core/server/middlewares/metrics.js)

