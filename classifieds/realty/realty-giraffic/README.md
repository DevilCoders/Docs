# Жирафик 

[Док](https://wiki.yandex-team.ru/vertis/vertistraf-dev/zhirafik/)
[Дашборд](https://grafana.vertis.yandex-team.ru/d/B6NUxbKnz/giraffic-dashboard?orgId=1)


# Локальный конфиг

1. Запустить из корня репозитория
```commandline
scripts/make_local_config.sh realty-giraffic/src/main/resources/giraffic.conf realty-giraffic
```
2. Поменять переменные
```
common.alloc.folder = /tmp
ops.port = "8081"
http.port = "8080"

jaeger.agent = null
```


### FAQ
#### После `makeLocalConfig` приложение не стартует

Нужно в локальном конфиге проставить **вместо** тех, что там есть
```
common.alloc.folder = /tmp
jaeger.agent = null
```
