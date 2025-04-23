# Сервис мониторинга времени билда андроид приложения Авто.ру


[Дашборд времени билда](http://ara-build-monitoring-graphana.vrts-slb.test.vertis.yandex.net/d/F9jppxQiz/talaiot) (логин/пароль:`root/root`)

## Запуск локально

Собираем образ командой 
```
docker build -t registry.yandex.net/vertis/ara-build-monitoring .
```
Запускаем его, предоставив порты для метрик `81` графаны `3003` и influxdb `8086`
```
docker run -p 81:81 -p 8086:8086 -p 3003:3003 registry.yandex.net/vertis/ara-build-monitoring
```

## Выкладка

Собираем образ командой
```
docker build -t registry.yandex.net/vertis/ara-build-monitoring .
```
пушим в registry командой
```
docker push registry.yandex.net/vertis/ara-build-monitoring
```
Перевыкладываем через бота или админку используя версию `latest`

## Полезные ссылки

- [Админка сервиса в vertis-admin](https://admin.vertis.yandex-team.ru/services/ara-build-monitoring)
- Имя докер-образа в registry: `registry.yandex.net/vertis/ara-build-monitoring`
- Адрес для подключения к InfluxDB: `http://ara-build-monitoring-graphana.vrts-slb.test.vertis.yandex.net:80`
- [Статус](https://grafana.vertis.yandex-team.ru/d/000000228/nomad-services-statistics?orgId=1&refresh=30s&var-datasource=Prometheus-testing&var-job=ara-build-monitoring&var-task=ara-build-monitoring-task&var-alloc_id=All&var-group=All&var-dc=All&var-host=All&var-average_interval=1m) контейнера в Nomad (потребляемые ресурсы и статистика ребутов):
