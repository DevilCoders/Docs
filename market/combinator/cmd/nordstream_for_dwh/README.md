# nordstream для аналитиков
1. [Здесь можно почитать про задачу](https://st.yandex-team.ru/COMBINATOR-3745) и [здесь](https://st.yandex-team.ru/COMBINATOR-3935)
2. [Здесь про формат данных](https://wiki.yandex-team.ru/market/development/combinator/nordstream/#dannyedljadwh/analitikov)

## Что это
Данные nordstream для аналитиков.
Оригинальный nordstream это BLOB таблица в YT.
Поэтому с ней трудно/невозможно работать через YQL.

Где данные:
1. [hahn prod](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/combinator/export/nordstream_for_dwh/recent)
2. [arnold prod](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/combinator/export/nordstream_for_dwh/recent)
3. [hahn test](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/testing/indexer/combinator/export/nordstream_for_dwh/recent)
4. [arnold test](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/testing/indexer/combinator/export/nordstream_for_dwh/recent)

## Как
Задача в sandbox, по расписанию.
1. [sandbox code](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/market/combinator/ExportNordstreamForDWH)
2. [scheduler](https://sandbox.yandex-team.ru/scheduler/710363/view)
3. [все ресурсы MARKET_NORDSTREAM_FOR_DWH_APP](https://sandbox.yandex-team.ru/resources?type=MARKET_NORDSTREAM_FOR_DWH_APP)

Задача запускает программу `nordstream_for_dwh`, использует последнюю версию ресурса.
Как залить новую версию ресурса:
```
cd market/combinator/cmd/nordstream_for_dwh
ya package pkg.json
ya upload --type MARKET_NORDSTREAM_FOR_DWH_APP nordstream_for_dwh.xxx.tar.gz
```
`nordstream_for_dwh` ходит по http в ручку комбинатора nordstream_for_dwh и записывает новую верисю данных в yt.

Запустить локально:
```
./run_app -local-dir pdata
./cmd/nordstream_for_dwh/nordstream_for_dwh -spec dev
```
В этом случае nordstream_for_dwh сходит в http://localhost:3000/nordstream_for_dwh и положит в //home/market/users/%user_name%/nordstream_for_dwh
