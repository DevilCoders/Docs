# grafana-infra-sync

grafana-infra-sync синхронизирует события из сервиса infra.yandex-team.ru в grafana.

### Графики
 https://grafana.vertis.yandex-team.ru/d/IxUnzQ9Wz/grafana-infra-sync?orgId=1&var-datasource=Prometheus

### Для локальной разработки
Создаем local.env и переопределяем там необходимые переменные из dev.env. 
А также прописываем в local.env секреты из https://yav.yandex-team.ru/secret/sec-01e4kexv0rp5w0172hwemzc1rf
