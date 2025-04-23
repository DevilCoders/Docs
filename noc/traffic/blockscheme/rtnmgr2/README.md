# Описание

Сервис ротации адресов для схемы обхода блокировок.  
Основное назначение: выделение для сервисов новых адресов из префиксов разных провайдеров (на момент написания это Telia и Cogent).  
DNS puller регулярно забирает список адресов и применяет их для прямых записей для UA view.

Основные компоненты:

- backend, предоставляющий;
- workers, используют API для запуска новой итерации ротации;
- агент, который применяет сгенерированные mapping-и.

# Сборка

Есть два механизма сборки:

- через docker-compose
- силами ya package

Docker-compose:

    docker-compose -f deployments/docker-compose.yml build
    docker-compose -f deployments/docker-compose.yml push

Ya package:

    ya package noc/traffic/blockscheme/rtnmgr2/deployments/api/package.json --docker --docker-repository mnt-traf/rtnmgr2 --docker-push
    ya package noc/traffic/blockscheme/rtnmgr2/deployments/workers/package.json --docker --docker-repository mnt-traf/rtnmgr2 --docker-push
