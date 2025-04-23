[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/scripts/grafana)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/scripts/grafana)

# Grafana

Набор скриптов для генерации дашбордов графаны и сенсоров EventDetector'а
EventDetector: https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/services/sre_tms/src/main/java/ru/yandex/market/sre/services/tms/eventdetector/

## Токены

Для деплоя дашбордов графаны используется АПИ, которое требует OAuth токен. Его нужно прописать в переменную окружения `GRAFANA_TOKEN`. Получить токен можно по ссылке 
https://oauth.yandex-team.ru/authorize?response_type=token&client_id=2a40092e5025480e99ec805b013f49cc

Для деплоя конфигов кликфита нужно прописать OAuth токен в переменную окружения `CLICKPHITE_TOKEN`. Получить по ссылке https://oauth.yandex-team.ru/authorize?response_type=token&client_id=05940c6441d549c685b3e6bdc097cd55


## Отладка

```bash
yammy run @yandex-market/grafana debug:build
```

### Отладка дашбордов

Для отладки дашбордов следует использовать скрипт `yammy run @yandex-market/grafana debug:dashboards` - он создаст и/или обновит все необходимые дашборды. Все отладочные дашборы персонализированы, так что вы не помешаете коллегам.

После завершения отладки стоит удалить дашборд в графане. Если дашборд потерялся его можно найти по тегу `debug--market-front-grafana`

### Отладка сенсоров

Для отладки сенсоров создан специальный дашборд на котором все сенсоры отображаются в виде графиков. Вся отладка идёт через него. 


### Отладка конфигов кликфита

Для отладки конфигов кликфита можно использовать как обычную так и debug сборку - разницы в них нет никакой. Для упрощения отладки рядом с конфигом создаётся одноимённый файл в формате markdown, который содержит общую информацию по содержимому конфига, а также диагностические запросы для отладки.

### Сборка

```bash
yammy build @yandex-market/grafana
```

Сборка выполняется автоматически в прекоммит-хуке. В ПРах проверяется, что результаты сборки были закоммичены в ветку, так что пропускать прекоммит не стоит. 

Чтобы добавить новый дашборд или сенсор в сборку надо прописать его в [список сборки](generate/)

Результаты сборки записываются в [generated/dashboards](generated/dashboards), [generated/sensors](generated/sensors), [generated/clickphite](generated/clickphite), [generated/metrics](generated/metrics), [generated/tables](generated/tables). Имя итогового файла берётся из названия поля в списке сборки. Конфиги кликфита, дашбóрды и сенсоры можно задеплоить, поэтому они игнорируются при коммите.

## Деплой

- Дашборды графаны деплоятся скриптом `yammy run @yandex-market/grafana deploy:dashboards`
- Конфиги кликфита деплоятся скриптом `yammy run @yandex-market/grafana deploy:clickphite`
- Сенсоры ивент детектора деплоятся скриптом `TICKET_KEY=MARKETFRONTECH-2102 DEPLOYMENT_DESC="Описание деплоя" yammy run @yandex-market/grafana deploy:sensors`

