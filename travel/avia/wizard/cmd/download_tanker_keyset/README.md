# Тулза для скачивания keyset-а с переводами из [Tanker](tanker.yandex-team.ru)

### Запуск
#### `Golang`
`Go Build configuration`:
* `Run kind: Directory`
* `Directory: $ARCADIA_ROOT/travel/avia/wizard/cmd/download_tanker_keyset`
* `Working directory: $ARCADIA_ROOT/travel/avia/wizard/cmd/download_tanker_keyset`
* Задать OAuth token для `Tanker` `Environment: TOKEN=` 
* Пример параметров запуска (значения по умолчанию):
    ```
    Program arguments: -branch_id go-wizard -project_id avia_wizard -keyset_id wizard -output wizard_default_keyset.json
    ```

#### `ya make`
* `ya make .`
* `./download_tanker_keyset -branch_id go-wizard -project_id avia_wizard -keyset_id wizard -output wizard_default_keyset.json`
