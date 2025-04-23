## deploy-status-exporter
Сервис для экспорта статуса деплоя (доступен/не доступен) из различных систем в Prometheus. 

### Сборка
```
docker build -t registry.yandex.net/vertis/deploy-status-exporter:<version> .
docker push registry.yandex.net/vertis/deploy-status-exporter:<version>
```

(Сервис максимально простой, если надо будет его менять несколько раз - то надо настроить сборку в тимсити)

### Деплой
https://admin.vertis.yandex-team.ru/services/deploy-status-exporter

Живет только в **проде**