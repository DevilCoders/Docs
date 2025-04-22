# Скрипты для создания Alert-ов в Solomone

## Prerequirements

Перед исползование установите [jq](https://stedolan.github.io/jq/)

*Mac OS X / Homebrew*

```
brew install jq
```

*Ubuntu*
```
apt-get install jq
```

Также необходимо получить токен для работы с API Solomon-а, и положить в файл `~/.solomon_token`
Токен можно получить по ссылке https://oauth.yandex-team.ru/authorize?response_type=token&client_id=1c0c37b3488143ff8ce570adb66b9dfa


## Как использовать

Все операции надо делать из директории `$ARCADIA/market/billing/infra/solomon/alert`, т.к. скрипты вызывают друг-друга.


### list_alerts.sh

Запускать без параметров, выводить список id-шек Alert-ов проекта market-billing


### show_alert.sh

При запуске без параметров показывает справку. Запускать указав `id` из предыдущего пункта
Можно записать в файл
```
./show_alert.sh market-billing-pg-disk-space-prediction > ./show_alert.sh market-billing-pg-disk-space-prediction.json
```


### dump_all_alerts.sh
Сохраняет все алерты проекта в директорию `./confs`, хорошо делать после массовых ручных изменений, чтобы закомить эти правки в VCS


### update_alert.sh
Для обновления сдампленного файла обновите сами файл, полученный запуском `show_alert.sh` или `dump_all_alerts.sh`, и запустите
```
./update_alert.sh <имя файла>
```

Например:
```
./update_alert.sh market-billing-pg-disk-space-prediction.json
```

### create_alert.sh

```
./create_alert.sh market-billing-pg-disk-space-prediction_updated.json
```

Создает новый алерт из файла, id алерта также береться из файла, поэтому если файл получен дампом существующего алерта в нем необходимо изменить `id` и убрать `version`


