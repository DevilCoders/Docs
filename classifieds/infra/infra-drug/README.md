# vertis-infra-docker

## структура проекта
- cmd/helper: хелпер для старт-стоп хуков деплоя в боксе сервиса
- cmd/infra: инфра-сервис для мониторинга, метрик и ручек готовности
- cmd/wrapper: обёртка для запуска сервиса с подмешшиванием переменных окружения предоставляемых shiva

## Конфиг
supervisor:
/etc/supervisord.conf

## Переменные окружения для запуска:
- CONSUL_ACL_TOKEN
- CONSUL_ENCRYPT
- CONSUL_ADDR
- SERVICE_NAME
- SERVICES_CONFIG_FILE - services definition json for consul
- CONTROLLER_PORT - controller listener port for pod hooks
- DC                          // - датацентр
- ENV                         // - окружение ( test,prod )
- REPORTER_GRPC_HOST_PORT     // - для jaeger ( dns:///jaeger-collector.service.consul:14250 )
- ADMIN_HTTP_PORT		      // - для jaeger ( 6835 )
- NOOB_SAIBOT_PORT            // порт для /metrics и /ping (5050)
- NOOB_SAIBOT_CHECK_INTERVAL  // интервал проверок (формат: 60s,1h, ...)
- CHECK_SERVICES              // список сервисов для проверки их живости ( для демо использовал consul-agent)
- HAPROXY_CONFIG              // url для скачивания конфигов haproxy
- HAPROXY_CONFIG_CHECK_INTERVAL // интервал проверки обновления конфига haproxy (формат: 30s)

## Пример запуска на тестовой тачке:
```
docker run -it -d --net=bridge  --hostname kasev-docker-01-dev.sas.yp-c.yandex.ne  -e "CONSUL_ACL_TOKEN=xxx" -e "CONSUL_ENCRYPT=yyy" -e "DC=sas" -e "ENV=test" -e "REPORTER_GRPC_HOST_PORT=dns:///jaeger-collector.service.consul:14250" -e "ADMIN_HTTP_PORT=6835"  docker_vertis_infra
```

## Как задеплоить в прод
- Собрать и пушшнуть докер-образ сайдкара: `APP_VERSION=ver make image push-image`
- Собрать и пушнуть helper-слой для бокса с сервисом: `make helper-layer`
- Зайти в sandbox-ресурс, посмотреть rbtorrent ссылку и вписать её [конфиг shiiva](https://github.com/YandexClassifieds/services/blob/master/deploy/shiva.yml) в переменную `DRUG_LAYER_INFRA_HELPER`
