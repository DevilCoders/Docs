## Обновление стрельб в ЦУМе

### Пререквизиты
Предварительно установить `jq`
```
https://stedolan.github.io/jq/download/
```

### Сборка pandora
Выолняем скрипт `./upload_pandora.sh`

Например вот так
```
➜  checkouter-production-fire ./upload_pandora.sh        
Ok
upload app/app
2910553911
upload cb_categories.json
2910554927
upload noncb_categories.json
2910555139
```

Указаные числа это id соответственных ресурсов

### Обновление local.yaml
Можно вопсользоваться скриптом `./resources.py update`
<details>
<summary>или руками</summary>

1. Проводим сборку и загрузку пандора через скрипт `./upload_pandora.sh`
2. Обновляем файл `tank.yaml`:
- по пути `pandora_cmd` пишем строку вида ` https://proxy.sandbox.yandex-team.ru/<resourceId>`, где `<resourceId>` - число из результата вызова скрипта `./upload_pandora` после строки `upload app/app`
- по пути `resources[0].src` - пишем строку вида ` https://proxy.sandbox.yandex-team.ru/<resourceId>`, где `<resourceId>` - число из результата вызова скрипта `./upload_pandora` после строки `upload cb_categories.json`, `resoruces[0].dst` - cb_categories.json
- по пути `resources[1].src` - пишем строку вида ` https://proxy.sandbox.yandex-team.ru/<resourceId>`, где `<resourceId>` - число из результата вызова скрипта `./upload_pandora` после строки `upload noncb_categories.json`, `resoruces[1].dst` - noncb_categories.json
</details>

#### Пример конфига (часть)

```yaml
pandora:
    resources:
        - src: https://proxy.sandbox.yandex-team.ru/2910554927
          dst: cb_categories.json
        - src: https://proxy.sandbox.yandex-team.ru/2910555139
          dst: noncb_categories.json
    pandora_cmd: https://proxy.sandbox.yandex-team.ru/2910484759
```