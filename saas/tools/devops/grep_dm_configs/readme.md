# Утилита для поиска заданных паттернов по конфигам saas-сервисов с возможностью их изменения и раскладывания по серверам

Пример использования:
```
./grep_dm_configs --name-pattern 'rtyserver.' --content-pattern 'DbgReqsThreads'
```

Пример вывода:
```
ydo_search_lb/rtyserver.diff-ydo_search_lb:     //"BaseSearchersServer.DbgReqsThreads": "${(CTYPE==\'stable\' or CTYPE==\'stable_ydo\') and 6 or ((CTYPE==\'stable_hamster\' or CTYPE==\'stable_hamster_ydo\') and 9 or 1)}",
ydo_search_lb/rtyserver.diff-ydo_search_lb:     //"Searcher.HttpOptions.DbgReqsThreads": "9",
ydo_search/rtyserver.diff-ydo_search:     //"BaseSearchersServer.DbgReqsThreads": "${(CTYPE==\'stable\' or CTYPE==\'stable_ydo\') and 6 or ((CTYPE==\'stable_hamster\' or CTYPE==\'stable_hamster_ydo\') and 9 or 1)}",
ydo_search/rtyserver.diff-ydo_search:     //"Searcher.HttpOptions.DbgReqsThreads": "9",
```

Возможен поиск по нескольким паттернам сразу. Следующая строка найдет конфиги, в которых есть и `PersistentSearchBanOnEmptyIndex` и `SyncPath`:
```
./grep_dm_configs --name-pattern 'rtyserver.' --content-pattern 'PersistentSearchBanOnEmptyIndex' 'SyncPath'
```

С найденными в конфигах строками можно производить различные манипуляции (параметр `--action`)\
**Перед выполнением каких-либо действий (кроме чтения) важно убедиться, что ваш паттерн не находит ничего лишнего**\
Список доступных действий:
+ read — ничего не делать, действие по умолчанию
+ delete — удалить найденную строку целиком
+ replace — сделать замену, формат: replace:{pattern}:{replacement}

После изменения конфигов обычно хочется сделать deploy, для этого есть параметр `--deploy` (**обновляются только бэкенды `rtyserver`**)

Пример массового обновления конфигов (замена `Timeout` на `TimeoutSeconds`) с уведомлением об окончании процесса через `ya notify`:
```
echo "./grep_dm_configs --name-pattern 'rtyserver.' --content-pattern 'ResourceFetchConfig.SkyGet.Timeout\"' --action 'replace:Timeout:TimeoutSeconds' --deploy; ya notify 'Done configs update!'" > script.sh
chmod +x script.sh
screen -dmSL dm_configs_mass_update bash -c './script.sh'
```
