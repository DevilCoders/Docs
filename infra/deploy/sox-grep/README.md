# Sox-grep
Утилита для выгрузки информации о релизах для sox-сервисов

### Usage
1) Получите YP-токен по адресу: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=f8446f826a6f4fd581bf0636849fdcd7
2) Откройте командную строку. Под windows для этого нужно ввести cmd в адресную строку проводника (windows explorer folder).
3) Добавьте токен в переменные окружения, для этого выполните команду:
```
set YP_TOKEN={token-here}
```
4) Запустить программу в директории где расположен скачанный файл:

    Нужно передать stage-id ИЛИ project-id, можно передать несколько значении разделив пробелами.

    По умолчанию, выгрузка производится о релизах за последние 3 месяца.
    Можно передать конкретный промежуток времени за который нужно выгрузить релизы (`--from-time` и `--to-time`) ИЛИ выгрузить релизы за последние N месяцев (`--last-n-months`).

    Переменные `--to-time` и `--from-time` принимают дату в формате `YYYY-MM-DD`.

    `--last-n-months` - целое число.

    Формат вывода определяется параметром `--format`: `csv` (по умолчанию) или `table`.

    ```
    grep-without-yp --project-id {PROJECT_ID} --stage-id {STAGE_ID} --from-time {FROM_TIME} --to-time {TO_TIME} --format {FORMAT}
    ```


#### Примеры:

1) С project-id за последние 3 месяца:
```
grep-without-yp --project-id my_project1 my_project2
```
2) stage-id и за последние 4 месяца как таблица:
```
grep-without-yp --stage-id my_stage_id --last-n-months 4 --format table
```
3) За период времени как csv, сохранив в файл `output.csv`:
```
grep-without-yp --stage-id my_stage_id1 my_stage_id2 --from-time 2001-01-22 --to-time 2020-02-01 --format csv > output.csv
```

### Вывод:
 Выгрузка в формате csv или таблица: идентификатор стэйджа(stage-id),
 дата создания деплой тикета(creation-time),
 тип релиза(release-type), список логинов, подтвердивших релиз(approved-users),
 ссылка на тикет(ticket-link)
