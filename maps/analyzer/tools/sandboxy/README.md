Простая обёртка над REST-api для чтения и обновления параметров шедулеров.
При попытке обновить PRODUCTION шедулер проверит, что в TESTING есть уникальный шедулер, для которого найдется хоть одна SUCCESS задача, и параметры у нее будут совпадать с обновляемыми.

# Релизы

Для просмотра статуса и выкладывания новых версий есть две команды: `info` и `release`.<br>
Первая выводит информацию о текущем статусе и ревизиях соответствующих шедулеров. В качестве аргумента опционально принимает основной тег шедулера (уникальный). Также можно передать теги и через повторяющийся аргумент `--tag`. Если не передавать вообще - выведет все задачи.

```bash
$ ./sandboxy info offline-eta-quality -v
offline-eta-quality
╒════════════╤════════════╤══════════╤═════════════════════╤═════════════╤═════════════════════╤═════════════════════════════════════════════════════╕
│            │   revision │ status   │ last run            │ last task   │ next run            │ url                                                 │
╞════════════╪════════════╪══════════╪═════════════════════╪═════════════╪═════════════════════╪═════════════════════════════════════════════════════╡
│ PRODUCTION │    7100751 │ WATCHING │ 2020-07-22 00:00:25 │ EXECUTING   │ 2020-07-22 12:00:00 │ https://sandbox.yandex-team.ru/scheduler/12979/view │
├────────────┼────────────┼──────────┼─────────────────────┼─────────────┼─────────────────────┼─────────────────────────────────────────────────────┤
│ TESTING    │    7100751 │ WATCHING │ 2020-07-20 23:30:19 │ EXECUTING   │ 2020-07-21 23:30:00 │ https://sandbox.yandex-team.ru/scheduler/12978/view │
╘════════════╧════════════╧══════════╧═════════════════════╧═════════════╧═════════════════════╧═════════════════════════════════════════════════════╛
```

В `info` можно не передавать тег, тогда выведется информация обо всех шедулерах. При этом лучше не указывать флаг `--verbose` (`-v`), так как такая команда медленнее (запрос на каждый шедулер), но без этого флага не будет выведена ревизия.

Для релиза в тестинг используется команда `release testing [TASK]`. Примеры:
* `release testing offline-eta-quality --revision r7100751` - выставить ревизию 7100751 в тестинге (можно указать как r7100751, так и 7100751)
* `release testing offline-eta-quality --set --binary_params "--statbox"` - обновить параметр шедулера (всё, что после `--set`, воспринимается как параметры для обновления)

Ревизия - это просто параметр шедулера, так что его тоже можно перечислить после `--set` (но тогда без префикса `r`), отдельный аргумент заведён просто для удобства.

Для релиза в прод используется команда `release production [TASK]`, при этом будет произведена проверка, что в тестинге был успешный запуск с такими же параметрами.

# Низкоуровневые команды

Эти команды ничего не знают про тестинг и продакшн, потому редкатировть с их помощью не рекомендуется.

Перечислить `id` всех шедулеров из тестинга:
```bash
$ ./bin/sandboxy list --testing
18608 | [TESTING] prepare-jams-level-history | robot-jams-testing | WAITING | SUCCESS
17279 | [TESTING] fix-legacy-tracks | robot-jams-testing | WAITING | SUCCESS
16987 | [TESTING] prepare-training-routes | robot-jams-testing | WAITING | FAILURE
...
```

Прочитать параметры:
```bash
$ ./bin/sandboxy read --tag prepare-matched-data --testing
12772 | [TESTING] prepare-matched-data | robot-jams-testing | WAITING | SUCCESS
https://sandbox.yandex-team.ru/scheduler/12772/view
------------------------------
environment : radio = testing
build_path : string = maps/analyzer/sandbox/prepare_matched_data/pkg
binary_path : string = maps/analyzer/sandbox/prepare_matched_data/pkg/maps/analyzer/sandbox/prepare_matched_data/sandbox/prepare_matched_data
binary_params : string =
ecstatic_dataset_name : string =
revision : integer = 6082022
vault_owner : string = robot-jams-testing
yql_token_vault_name : string = YQL_TOKEN
yt_token_vault_name : string = YT_TOKEN
statbox_token_vault_name : string = STATBOX_TOKEN
yavault_token_vault_name : string =
```

Обновить ревизию (всё, что после `--set`, воспринимается как параметры для обновления):
```bash
$ ./bin/sandboxy update --tag prepare-matched-data --testing --set --revision 6082023
```

Обновить ревизию всех шедулеров в тестинге (чтобы не обновить всем случайно, в данном случае требуется аргумент `--batch`, показывающий, что команда будет применяться ко многим шедулерам):
```bash
$ ./bin/sandboxy update --testing --batch --set --revision 6082023
Updating 18608 ([TESTING] prepare-jams-level-history) to set revision=6082023...
Updating 17279 ([TESTING] fix-legacy-tracks) to set revision=6082023...
Updating 16987 ([TESTING] prepare-training-routes) to set revision=6082023...
...
```

Также можно указать аргумент `--dry`, чтобы просто узнать, какие шедулеры будут обновлены:
```bash
$ ./bin/sandboxy update --testing --dry --batch --set --revision 6082023
Going to update 18608 ([TESTING] prepare-jams-level-history) to set revision=6082023...
Going to update 17279 ([TESTING] fix-legacy-tracks) to set revision=6082023...
Going to update 16987 ([TESTING] prepare-training-routes) to set revision=6082023...
...
```
