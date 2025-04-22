## Формат названий для файлов в tools/transport-spb/data

manual-changes-Vyyyy-MM-dd.csv
threads-actual-Vyyyy-MM-dd.json
threads-future-Vyyyy-MM-dd.json

## 2 шага на пути к успеху:

### 1. поматчи данные:

1. положи исходные данные в `tools/transport-spb/data` с отформатированным именем (не забываем поменять .geojson на .json и добавить дефисы в дату)
2. вызови `make match`

### 2. загрузи данные:

1. см. [prerequisite](#bunker-details) 1 и 2 пункт
2. проверь, что файлы routes.json and changes.json в папке с датой последнего изменения данных в названии
3. вызови `make upload ARGS="NODE_ENV=testing"`
4. см. [prerequisite](#bunker-details) 4 пункт
5. повтори 3 и 4 пункт для `ARGS="NODE_ENV=production"`

## debug:

(все команды make должны быть вызваны внутри папки tools/transport-spb)
(все относительные пути должны строиться относительно tools/transport-spb baseUrl)

### команды матчинга данных:

1. `make collapse-actual-threads` optional params: actualThreadsFile=${path to actual threads file}
2. `make collapse-future-threads` optional params: futureThreadsFile=${path to future threads file}
3. `make transform-routes-to-maps-format` optional params: collapsedActualFile=${path to collapsed actual file from step #1}, collapsedFutureFile=${path to collapsed future file from step #2}
4. `make get-stand-data` optional params: routesFile=${path to transformed routes file from step #3} csvFile=${path to .csv file}

### команды проверки данных

5. `make get-diff-between-routes-and-changes` optional params: dataDir=${data dir path from step #4}
6. `make check-data` optional params: dataDir=${data dir path from step #4}
7. `make find-similar-to-empty-routes` optional params: dataDir=${data dir path from step #4}

### команды загрузки данных

8. `make routes-upload ` optional params: dataDir=${data dir path from step #4}
9. `make changes-upload` optional params: dataDir=${data dir path from step #4}

### Как вызвать команду с аргументами:

`make ${command} ARGS='${parameter}=${value}'`

## troubleshooting:

### if make script doesn't work properly:

`NODE_PATH=./ npx ts-node ${full relative path to .ts file} ${args}`

## bunker-details.

1. Если в родительской ноде ([Бункер Тестинг](https://bunker.yandex-team.ru/maps-www/testing/transport-spb), [Бункер Прод](https://bunker.yandex-team.ru/maps-www/production/transport-spb)) нет ноды superimposed-lines-routes то надо её создать.
2. В ноде superimposed-lines-changes хранится актуальный список изменений маршрутов с их id, так что старые ноды маршрутов не зааффектят отображение данных (их можно не удалять). Изменённые (не удалённые) данные по маршрутам обновятся, только если они отличаются от тех, что сейчас лежат в бункере (например, приехал новый файл routes - изменённые данные маршрутов обновятся, а те, которые не изменились - аплоадиться не будут (сравнение через isEqual)). С неактуальными нодами ничего не происходит - они так и лежат в superimposed-lines-routes, но т.к. их id нет в superimposed-lines-changes, то на стенде они не окажутся (запрос данных о маршруте происходит по id из списка changes).
3. Проверить, что в `tools/transport-spb/get-stand-data/data/${last data update date}` лежат файлы routes.json и changes.json и они валидны
4. `make upload NODE_ENV=testing`. **_Внимание!_** для загрузки маршрутов тестинг или продакшен нужно указать NODE_ENV при запуске (testing или production). Также можно обновить какие-то конкретные данные с помощью команд `make routes-upload NODE_ENV=testing` и `make changes-upload NODE_ENV=testing`
5. В итоге надо запаблишить изменения (superimposed-lines-routes и superimposed-lines-changes) в интерфейсе бункера. **_Внимание!_** При паблишинге routes не забудьте инкрементировать руками версию в режиме RAW (чтобы стала доступна кнопка publish), а также поставить галочку recursive - иначе сами ноды маршрутов не запаблишатся.
