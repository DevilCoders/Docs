# Утилита для генерации сниппетов masstransit/2.x

Эта программа генерирует сниппеты masstransit/2.x для геопоиска. Информация о самом сниппете есть на вики: https://wiki.yandex-team.ru/maps/dev/core/masstransit/api/snippeter/#masstransit/2.x.

Общая схема такая:

1) Эта утилита генерирует таблицу YT, в которой каждая строка содержит идентификатор некоторого географического объекта и сниппет для этого объекта. Готовая таблица для продакшена лежит тут: https://yt.yandex-team.ru/hahn/navigation?path=//home/yatransport-prod/production/snippets/latest/snippets&offsetMode=row
2) Sandbox-задача Task Manager (https://wiki.yandex-team.ru/users/karas-pv/snippetstaskmanager/) каждую ночь заливает содержимое этой таблицы в геопоисковый SaaS.
3) Когда геопоиск формирует ответ на поисковый запрос, он для каждого объекта выдачи проверяет, есть ли в SaaS сниппет для этого объекта. Если есть, то поиск добавляет информацию из сниппета в свой ответ.

Сниппеты генерируются для двух категорий объектов:

- Организации справочника. Берутся вот из этой таблицы: https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/altay/prod/snapshot/company&offsetMode=row. Ключом в таблице со сниппетами является `permalink` организации.
- Адреса, например "Льва Толстого, 16". Берутся из таблиц addr в YMapsDF https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest. Ключом является строка `geocoder_id_<addr_id>`, где `<addr_id>` - поле из таблицы addr.

Эта утилита запускается раз в день из сендбокса задачей [MapsMasstransitBuildSnippets](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/masstransit/MapsMasstransitBuildSnippets?rev=4973511). Задача запускает утилиту с последним релизом [MASSTRANSIT_DATA](https://sandbox.yandex-team.ru/resources?type=MASSTRANSIT_DATA&limit=20) из сендбокса и соответствующим ему [пешеходным графом](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/pedestrian_graph) из YT. Ссылка на шедулер: https://sandbox.yandex-team.ru/scheduler/14429/view.

Конфиг task manager'а тут: https://a.yandex-team.ru/arc/trunk/arcadia/search/geo/tools/task_manager/configs/task_manager.json?rev=4999579#L487

## Как получить сниппет из поиска

Запрос для топонима:
```
http://addrs-testing.search.yandex.net/search/stable/yandsearch?origin=alf&ll=37.6,55.7&spn=1,1&text=Льва+Толстого,16&type=geo&snippets=masstransit/2.x&ms=pb&hr=yes&results=1
```
В ответе нужно смотреть на секцию `yandex.maps.proto.search.masstransit_2x.GEO_OBJECT_METADATA`:
```
stop {
    stop {
    id: "station__9858874"
    name: "Парк культуры"
    }
    point {
    lon: 37.592872436
    lat: 55.73530476
    }
    distance {
    value: 392.258
    text: "390 м"
    }
    line_at_stop {
    line {
        id: "100000088"
        name: "Кольцевая линия"
        style {
        color: 8323072
        }
        vehicle_types: "underground"
    }
    }
}
...
```

Запрос для организации:
```
http://addrs-testing.search.yandex.net/search/stable/yandsearch?origin=alf&ll=37.6,55.7&snippets=masstransit/2.x&ms=pb&hr=yes&uri=ymapsbm1://org?oid=1101237450&spn=1,1&mode=uri&results=1
```

## Как выкатывать программу

Чтобы выкатить новую версию этой утилиты, нужно собрать ее задачей YA_MAKE, указав тип ресурса [MAPS_MASSTRANSIT_BUILD_SNIPPETS_TOOL_BINARY](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/masstransit/MapsMasstransitBuildSnippets/__init__.py?rev=4973511#L20). Для этого можно просто запустить шедулер https://sandbox.yandex-team.ru/scheduler/14534/view. Получившийся ресурс с бинарем надо зарелизить в stable. Задача, запускающая сборку сниппетов, автоматически подхватывает последний released бинарь.

Перед выкладкой новой версии стоит вручную запустить программу и убедиться, что она не падает и результирующая таблица со сниппетами похожа на правильную. Я запускаю примерно так:
```
./build-snippets --masstransit-data ~/yandex-maps-masstransit-data_22.06.01-2/static.fb --graph //home/maps/core/garden/stable/pedestrian_graph_fb/22.06.01-2 --working-dir "//home/yatransport/user/snippets"
```

## Тестовый сниппет

Если хочется что-то поменять в содержимом сниппетов, то перед релизом изменений имеет смысл проверить, что новые сниппеты нормально работают. Для этого есть тестовый сниппет [masstransit_test/2.x](https://a.yandex-team.ru/arc/trunk/arcadia/search/geo/tools/task_manager/configs/task_manager.json?rev=4999579#L477). Этот сниппет каждый день обновляется в SaaS из таблицы https://yt.yandex-team.ru/hahn/navigation?path=//home/yatransport-prod/testing/snippets/latest/snippets&offsetMode=row. Тестовым сниппетом никто не пользуется, поэтому туда можно небоясь залить все что угодно и проверить курлом, что при запросе этого сниппета поиск отдает ожидаемый результат. Сниппеты доставляются в поиск ночью, поэтому после сборки таблицы протестировать сниппеты можно будет только на следующий день.

Чтобы получить тестовый сниппет из поиска, надо в запросе заменить `masstransit/2.x` на `masstransit_test/2.x`:
```
http://addrs-testing.search.yandex.net/search/stable/yandsearch?origin=alf&ll=37.6,55.7&spn=1,1&text=Льва+Толстого,16&type=geo&snippets=masstransit_test/2.x&ms=pb&hr=yes&results=1
```

**ВНИМАНИЕ:** В SaaS нет места на два полных набора сниппетов masstransit, поэтому из таблицы с тестовыми сниппетами в SaaS заливаются только первые 2.5 миллиона строк (это настраивается в конфиге таск менеджера). Утилиту можно запустить с флагом `--testing`, и тогда она соберет сниппеты только для Москвы - как раз 2.5 миллиона.

## Одноимённые станции

В сниппеты попадают станции метро на разных ветках с одинаковым названием. Иногда эти станции вытесняют другие из списка, так что для некоторых объектов показывается всего одна станция метро, но на разных ветках.
Для решения этой проблемы была разработана [версия](https://a.yandex-team.ru/arc/trunk/arcadia/junk/dranikpg/masstransit-snippets?rev=r8379458), которая объединяет одноименные станции на пересадочных узлах.
На данный момент эта версия не используется, поскольку такая логика менее понятна для многих пользователей. К такому выводу пришли в [этом тикете](https://st.yandex-team.ru/MTDEV-709).
