##Конфиги для [Monitorado](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/monitorado)

###
- `awacs.monitorado.yml` - мониторинги балансеров в AWACS
- `deploy.monitorado.yml` - мониторинги инстансов в Deploy
- `mdb.monitorado.yml` - мониторинги баз данных в MDB

### Применение мониторингов

1. Кладём [OAuth токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=171fcece39a04fd0a6b8b74950336008) в переменную окружения `MONITORADO_OAUTH_TOKEN`

1. Смотрим, какие изменения будут сделаны:

   `monitorado diff -v -c <config.monitorado.yml>`

1. Настраиваем мониторинги:

   `monitorado exec -v -c <config.monitorado.yml>`

1. Коммитим конфиг


## Шаблоны панелей yasm

- `progruzki.jinja2` - графики для отслеживания состояния сервисов Droideka, Updater, Report, Alice-proxy [yasm](https://yasm.yandex-team.ru/template/panel/droideka-progruzki/)
- `droideka-unistat.jinja2` - метрики сервиса Droideka [yasm](https://yasm.yandex-team.ru/template/panel/droideka-counters/)
- `alice-proxy-unistat.jinja2` - метрики сервиса Alice-proxy [yasm](https://yasm.yandex-team.ru/template/panel/alice-proxy-counters/)
