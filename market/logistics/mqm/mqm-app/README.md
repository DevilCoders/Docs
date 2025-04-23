# MQM

## Локальный запуск

**Локальные настройки (dev)** находятся в файле src/main/properties.d/local/application.properties.dist, который нужно
_скопировать_ в application.properties, рядом. Копию можно реадктировать по своему желанию, не добавляя в репозиторий.

_Новые настройки конфигураций нужно не забывать добавлять в dist._

### Общее

Параметры запуска в Идее должны быть следующими:
- **Main class:** ``ru.yandex.market.logistics.mqm.LogisticsMqm``
- **Working directory:** ``path_to_mqm_idea_project``
- **Environment variables:** ``PROPERTIES_DIR=/path_to_your_arcadia_or_svn_repo/market/logistics/mqm/mqm-app/src/main/properties.d``
- **Active profiles**: ``local``

###Развертка локальной бд (dev)

**NB:** Если вы пользуетесь Арком, папка должна быть смонтирована с параметром --allow-other, иначе ни docker ни liquibase не стартуют

Установить liquibase локально (не обязательно, можно использовать cli jar-ник из зависимостей проекта)

**Mac**: ``
brew install liquibase
``

**Ubuntu**:
``
sudo snap install liquibase --beta
``

Запустить контейнер с локальной бд (будет создана без миграций, они накатываются самим приложением)
```
docker-compose -f mqm-app/dependency-stubs/docker-compose.yml up -d
```
