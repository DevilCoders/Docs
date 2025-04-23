## Получение исторических данных по времени выполнения ci

1. Получить список сандбокс тасков `TRENDBOX_CI_JOB_BETA`, у которых в описании есть `push` и `morda/main`
2. Из ответа каждого таска вытащить
 - `output_parameters.logs_urls`
 - `intervals.{queue,execute}.duration`
 - `time.{created, updated}`
 - `trendbox_config.name`
3. Считаем метрики
 - общее время таска = `time.updated - time.created`
 - время в очереди = `intervals.queue.duration`
 - время выполнения =  `intervals.execute.duration`
 - из logs время install, prepare, script, beforeScript, afterScript
 - из logs.script время каждого tkit шага
4. Группируем по `name`
5. Пушим в стат деревом
```
 root
    |- queue
    |- execute
        |- install
        |- prepare
        |- beforeScript
        |- script
        |    |- ...tkit
        |- afterScript
```

### Использование

```
npm ci
STAT_TOKEN=<токен статфейса> npx ts-node ./grep-task-resources.ts --window <на сколько дней назад> --from <от какого времени искать>
```