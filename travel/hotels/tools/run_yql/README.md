### Что это

Данная утилита предназначена для запуска YQL скриптов, которые находятся в папке `queries`.

### Запуск YQL скрипта

Утилита принимает следующие параметры:
* `--yt-proxy` - Кластер YT, на котором будет исполняться запрос 
* `--yql-token` - токен YQL, обязательный параметр
* `--yt-token` - токен YT
* `--yt-token-path` - путь до токена YT
* `--versioned-path` - версионированный путь. 
  Если указан, то должен быть указан `yt-token` или `yt-token-path`. 
  Итоговый путь попадает в скрипт через подстановку `%VERSIONED_PATH%` в аргументах  
* `--query-name` - имя запроса из папки `queries`
* `--processor-name` - имя python скрипта с пре/пост процессором. По умолчанию проверяется `{query-name}.py`
* `--processor-args` - список аргументов процессора
* `--query-args` - список параметров для запуска скрипта в формате `ключ=значение`. Перед передачей в YQL в начало ключа приписывается символ `$`. 

Пример запуска:
```
./run_yql --yql-token <...> --query-name build_searchkey_restrictions.yql --query-args input_path_feed=//home/travel/prod/feeds/travelline/2020-06-26/parsed output_path_result_table=//home/travel/alexcrush/searchkey_restrictions/travelline
```

### Добавление нового скрипта

Всего два шага:

1. Положить скрипт в `queries`
2. Добавить его в секцию `RESOURCE` в ya.make

После коммита произойдет автосборка новой версии, и скрипт можно запускать через sandbox_planner, [пример](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/sandbox_planner/plan.yaml?rev=7051194#L330)  
