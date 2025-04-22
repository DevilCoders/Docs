Гео колдунщик, который показывается на серпе на запросах про маршруты (маршруты по городу, маршруты между городами), например: [маршрут москва тверь](https://yandex.ru/search/?lr=213&text=маршрут%20москва%20тверь), [как доехать от улицы льва толстого до ленинского проспекта](https://yandex.ru/search/?text=как%20доехать%20от%20улицы%20льва%20толстого%20до%20ленинского%20проспекта&lr=213) и т.д.
Выглядит следующим образом:
![колдунщик](https://jing.yandex-team.ru/files/ianaval/Screen%20Shot%202020-08-26%20at%204.36.25%20PM.png)

## Полезное
[Общее про колдунщики](https://wiki.yandex-team.ru/users/ianaval/serp-wizards/)

## Где живет
| Название | Примечание |
|----------|------------|
| [Код колдунщика](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/wizards/routes)| |
| [Конфиг источника в аппхосте](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/backends/WIZROUTES.json)| [Документация](https://doc.yandex-team.ru/apphost/pages/backends.html) |
| [Конфиг источника в вертикали WEB](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/WEB/web.json?rev=7306554#L6277)| [Документация](https://doc.yandex-team.ru/apphost/pages/nodes.html) |
| [Код бегемотного src_setup'а](https://a.yandex-team.ru/arc/trunk/arcadia/search/begemot/rules/src_setup/routes)| Здесь настраивается, какие параметры, разборы каких правил визарда передаются в колдунщик. Можно отфильтровать трафик от неподходящих запросов|
| [Сервис в няне](https://nanny.yandex-team.ru/ui/#/services/catalog/routes_proxywizard_yp) | |

## Как собирать и поднимать локально
1. Код колдунщика собирается командой ```ya make -r```
2. Из сервиса няни забираем конфиг ```apache.ywsearch.cfg```
([Files](https://nanny.yandex-team.ru/ui/#/services/catalog/routes_proxywizard_yp/files) -> прокручиваем в самый низ)
3. Выкачиваем себе ресурс ```GEODB_DATA``` (id ресурса опять же берем из няни), переименовываем в ```geodb.data```
4. Поднимаем командой
```bash
./routes -V Port=<port> -V EventLog=eventlog apache.ywsearch.cfg
```
5. При запросе с https://yandex.ru или https://hamster.yandex.ru подменяем на свой, для этого нужно дописать параметр: ```&srcrwr=WIZROUTES:host:grpc_port```, где ```grpc_port=port+2```

## Сборка бинарника в Sandbox
1. Для сборки бинарника есть специальный таск ```BUILD_WIZARD_PROXY```, [пример таска](https://sandbox.yandex-team.ru/task/551773534/view).
2. Его можно склонировать, указать нужную ревизию и поставить флажок напротив ```build_routes```
3. На выходе таска получается ресурс ```PROXY_WIZARD_ROUTES_EXECUTABLE```
4. Дальше этот ресурс можно зарелизить в ```stable``` и выкатить в няне. Чтобы можно было релизить, нужны [права](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/common/proxy_wizard/executable_types.py?rev=7310925#L82) на это.

## Графики
| Название | Примечание |
| -------- | ---------- |
| [Графики аппхоста](https://yasm.yandex-team.ru/menu/apphost/WEB/web/WIZROUTES/) | Тут можно смотреть тайминги ответа аппхосту |
| [Графики колдунщика](https://yasm.yandex-team.ru/chart/itype=proxywizard;ctype=prestable,prod;prj=routes-proxywizard-yp;hosts=ASEARCH;graphs=%7Bunistat-num_requests_dmmm,unistat-num_errors_dmmm,unistat-num_successes_dmmm%7D/) | rps |
| [Профицит](https://solomon.yandex-team.ru/?project=blender&cluster=production&service=surplus&l.serp_type=desktop%7Ctouch&l.kind=win-minus-loss*&l.prefix=wiz&l.domain=ru&l.version=v6.1.b&l.pixel=pixel&l.name=route&graph=auto&stack=false&checks=-&autorefresh=y&b=365d&e=) | Периодически выходят новые версии профицита, поэтому график может резко обрываться. В таком случае скорее всего нужно выбрать новую версию профицита. |
| [Трафик](https://datalens.yandex-team.ru/a9tdtbo8g8x46-performance-geoservices?tab=8l) | Трафик на карты с разных гео колдунщиков|`
