# Тулза для обновления keyset-а с переводами в [Tanker](tanker.yandex-team.ru)

### Запуск
#### `Golang`
`Go Build configuration`:
* `Run kind: Directory`
* `Directory: $ARCADIA_ROOT/travel/avia/wizard/cmd/replace_tanker_keyset`
* `Working directory: $ARCADIA_ROOT/travel/avia/wizard/cmd/replace_tanker_keyset`
* Задать OAuth token для `Tanker` `Environment: TOKEN=` 
* Пример параметров запуска (значения по умолчанию):
    ```
    Program arguments: -branch_id go-wizard -project_id avia_wizard -keyset_id wizard -input wizard_default_keyset.json
    ```

#### `ya make`
* `ya make .`
* `./replace_tanker_keyset -branch_id go-wizard -project_id avia_wizard -keyset_id wizard -input wizard_default_keyset.json`
