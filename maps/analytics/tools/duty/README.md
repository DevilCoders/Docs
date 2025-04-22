# duty

`CLI` утилита, запускающая набор тасков, облегачающих жизнь дежурным

## Таски
* `linker` — линкует инциденты, созданнные за последние 30 часов, к тикету дежурства
* `description` — форматирует описание задачи в трекере, созданнные за последние n минут
* `description_cofe` — форматирует описание задачи cofe в трекере, созданнные за последние n минут
* `duty_doc` — добавляет в описание задачи в трекере документацию по починке расчетов
* `error_log` — добавляет в описание задачи в трекере логи упавших кубиков нирваны
* `delay` — добавляет в описание задачи в трекере информацию о задержавшихся расчетах
* `autoclose` — автоматически пингуются и закрываются delay задачи в трекере, которые пофиксились
* `restart` — таска, которая добавляет в тикет кнопку перезапуска упавшей реакции


### linker 

Таска, которая будет линковать все тикеты мониторинга к тикету дежурного


### description

Основополающая таска, которая преобразует описание в UX-friendly

**ВАЖНО!! Без этой таски, остальные нижестоящие таски нет смысла запускать, они все зависят от преобразований этой**

### duty_doc
Таска, которая прикладывает документацию. Нужно указать файл md, который написан в определенном формате:
```md
### some_regexp

- Нужно сделать то и это
- Написать в чат ….
```

Парсит по `###` и матчит(`re.search`) с названием тикета

Для добавления своей документации, нужно [добавить](https://a.yandex-team.ru/arc_vcs/maps/analytics/tools/duty/lib/ya.make?rev=r9411238#L12) ее в `ya.make`

### restart (пока только для аналитики карт)

Добавляет в тикет форму с кнопкой https://forms.yandex-team.ru/surveys/101863. По нажатии на кнопку генерируется артефакт и перезапускается эта же таска, которая сделает `clone` последней (упавшей) реакции

## Разработка
Для разработки нужно задать следующие токены:
- `STARTREK_TOKEN` - токен для трекера
- `NIRVANA_TOKEN` - токен для Нирваны

Запуск происходит из папки `bin` в два шага:
- `ya make`
- `rlwrap ./bin` (`rlwrap` нужен для нормального дебага в консоли)

Запустить локально можно в одну строчку: 

`ya make && rlwrap ./bin --tasks error_log --tracker-monitoring-queue GEOMONITORINGS --duty-doc-path maps/analytics/docs/duty.md --tracker-duty-components Дежурство --tracker-duty-queue GEOANALYTICS --tracker-components maps-analytics geodisplay-analytics`

...в том числе и на конкретный тикет и конкретную таску:
`ya make && rlwrap ./bin --tasks error_log --tracker-monitoring-queue GEOMONITORINGS --duty-doc-path maps/analytics/docs/duty.md --tracker-duty-components Дежурство --tracker-duty-queue GEOANALYTICS --tracker-components maps-analytics geodisplay-analytics --tracker-issue-key TEST-259597`


[Документация](https://a.yandex-team.ru/arc/trunk/arcadia/library/python/yandex_tracker_client/README.rst) по либе трекера 


## Продакшн

```bash
./bin
    --tasks description duty_doc
    --tracker-monitoring-queue GEOMONITORINGS
    --tracker-components maps-analytics geodisplay-analytics
    --tracker-duty-queue GEOANALYTICS
    --tracker-duty-components Дежурство
    --duty-doc-path maps/analytics/docs/duty.md
```
