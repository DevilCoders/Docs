# Выкладка пакета yandex-search-salt
После сборки свежей версии yandex-search-salt создаем PR в saltstack в develop с новой версией в common/deploy/ya-salt/stages.yaml.

    prestable:
      share: 100
      version: "2.0-<new-revision>"
    stable:
      share: 100
      version: "2.0-<old-revision>"
    default:
      version: "2.0-<old-revision>"

Дальше, если проверка на prestable  показала, что все работает как нужно, выкатываем пакет на остальные контура.
После окончания выкладки на master_msk, если ничего не сломалось, нужно переложить версию, которую выкатили в stable ветку репозитория.

    ssh duploader.yandex.ru sudo dmove search stable yandex-search-salt 2.0-<new-revision> unstable

Перемещение пакета в stable и проверку, что хосты с новой версией успешно переналиваются, выполняет инициатор выкладки.


## Настройки автоочистки
Автоматика очистки настраивается в конфигах сервиса https://nanny.yandex-team.ru/ui/#/services/catalog/dist_duploader.
Конфигурация состоит из двух частей.

    # https://nanny.yandex-team.ru/ui/#/services/catalog/dist_duploader/files#repo-cleaner-search.sh
    
    #!/bin/bash

    set +e
    
    mkdir -p "$CLEANER_DIR/search"
    
    sudo cacus repo-cleaner prepare --repos-config cleanup.yaml --repo search --output-dir "$CLEANER_DIR/search"
    sleep 10
    sudo cacus repo-cleaner apply --batch "$CLEANER_DIR/search/search.yaml" --keep-going --yes-i-really-want-lsr-ticket
    sleep 10
    
    exit 0

Скрипт запуска repo-cleaner меняется почти никогда, а вот секция конфига https://nanny.yandex-team.ru/ui/#/services/catalog/dist_duploader/files#cleanup.yaml может меняться.

    repos:
    
    ...
    
      search:
        keep_time: any
        keep_last_versions: any
        branches:
          stable:
            keep_time: any
            keep_last_versions: any
            packages:
              yandex-search-salt:
                keep_time: any
                keep_last_versions: 10
          unstable:
            keep_time: any
            keep_last_versions: any
            packages:
              yandex-search-salt:
                keep_time: any
                keep_last_versions: 30

Немного подробнее про repo-cleaner можно почитать в https://wiki.yandex-team.ru/runtime-cloud/services/dist/#cacusrepo-cleaner
