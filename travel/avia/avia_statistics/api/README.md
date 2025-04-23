avia-statistics api
--------

### Локальная разработка
Скачать справочники расписаний:
```shell
cd travel/avia/avia_statistics/api
sh tools/download_dicts.sh
```

В Goland нужно настроить build-configuration:
  0. `Run | Edit configurations... | Add | Go Build `
  1. `Run kind: Directory`
  2. `Directory: $ARCADIA_ROOT/travel/avia/avia_statistics/api/cmd/api`
  3. `Working directory: $ARCADIA_ROOT/travel/avia/avia_statistics/api`
  4. В `Environment:` добавить `CONFIG_PATH=./dev/config.development.yaml`
  5. Положить dev-конфиг в `Working directory` из пункта 3 и прописать все секреты:
     ```shell
     cd $ARCADIA/travel/avia/avia_statistics/api
     cp config/config.development.yaml dev
     vim dev/config.development.yaml
     ```

Если при билде возникают ошибки про `No Go files in directory ...` нужно выполнить:
```
cd /travel/avia/avia_statistics/api
ya make --yt-store --add-result=.go
```
