## Eventlog и обстрелы

`EntitySearch` на продовых машинках запускается с ключом `-l` (или `--log`) и [логирует](https://a.yandex-team.ru/arc/trunk/arcadia/search/wizard/entitysearch/service/server.cpp?rev=7488457#L1983) присылаемые ему аппхостовые контексты. Эти контексты можно переиспользовать для проверки своих изменений в условиях, максимально приближенных к реальным.

### Как достать eventlog с продовой машинки
* Заходим на любую машинку в няне (например, [VLA](https://nanny.yandex-team.ru/ui/#/services/catalog/vla-production-entitysearch-yp/) -> Instances -> Access -> SSH)
* Находим, куда пишется `eventlog`: `ps aux | grep './entitysearch'`
* Копируем найденный файл с помощью `scp` (не забудьте добавить флаг `-A` при логине через SSH!). Количество контекстов можно грубо оценить как размер файла в байтах, поделенный на ~20000.

### Как превратить бинарный файл во что-то человекочитаемое
* Дампер отфильтровывает события `ReqWizardRequestReceived`, разворачивает их в `json` и кладет в табличку на `YT` три поля -- `RequestId`, `Base64Context` и `JsonContext`.
* Самый простой вариант использования: `ya upload {eventlog}` и [кубик](https://nirvana.yandex-team.ru/operation/11c6481f-434a-4941-bd3e-459c8661e06f) в нирване.
* Можно сделать то же самое локально (`ya make -r && ./evlogdump --help`), только помните, что `eventlog` процессится последовательно и может долго висеть -> используйте tmux.
    Параметры специально упрощены до максимума, если вам нужны более тонкие настройки дампера, смотрите [сюда](https://a.yandex-team.ru/arc/trunk/arcadia/library/cpp/eventlog/dumper/evlogdump.cpp?rev=7517056#L125).

### Как заслать контекст в поднятую бету
* Собираем `servant_client`: `cd $ARCADIA/apphost/tools/servant_client && ya make -r --dist -E`
* Берем любой `Base64Context` из таблички на `YT` и стреляем: `./servant_client -t bin host:apphost_port/serp ctx.bin >> response.json`
    Достать любой произвольный `Base64Context` из таблички можно, например, так: `yt read --table //home/path/to/table[#0:#1] --format '<encode_utf8=%false>json' | jq .Base64Context > ctx.bin`
    Все то же самое можно сделать при помощи `JsonContext`, только без опции `-t bin`.
* Можно сделать то же самое через `python requests`, только засылать нужно `post` запрос с `data=base64.b64decode(Base64Context)`
* `servant_client` вернет нам еще один аппхостовый контекст, сгенерированный поднятой бетой.
    Сам `EntitySearch` отдает данные в [формате](https://a.yandex-team.ru/arc/trunk/arcadia/search/idl/meta.proto?rev=7468923#L41) `NMetaProtocol::TReport`.

### Как распарсить `NMetaProtocol::TReport`
* Собираем `app_host_ops`: `cd $ARCADIA/search/tools/app_host_ops && ya make -r --dist -E`
* Запускаем `./app_host_ops print-context -t service_response -i response.json >> parsed.json` или все вместе -- `./servant_client host:apphost_port/serp ctx.json | ./app_host_ops print-context -t service_response >> parsed.json`. Теперь `TReport` из `proto` превратился в `json`.

### Как достать ответ самого `EntitySearch`
* `cat parsed.json | jq '.answers | .[] | select(.type == \"ENTITYSEARCH\")'`

### Как достать данные, которые отправляются на верхний
* `cat parsed.json | jq '.answers | .[] | select(.type == \"ENTITYSEARCH\")' | jq .binary.data.Grouping[0].Group[0].Document[0].ArchiveInfo.GtaRelatedAttribute | jq '.[] | select(.Key == \"_SerpData\") | .Value'`
    `_SerpData` -- классический пример `json`-a внутри `json`-a, поэтому его неплохо бы распарсить еще раз. У меня не получилось сделать это с помощью `jq`, поэтому можно в конце сделать так: `| python3 -c 'import json, sys; print(json.loads(sys.stdin.read() or "{}"))'`

### Как достать онтоиды всех объектов в карусели ОО
* `cat parsed.json | jq '.answers | .[0] | select(.type == "ENTITYSEARCH")' | jq .binary.data.Grouping[0].Group[0].Document[0].ArchiveInfo.GtaRelatedAttribute | jq '.[] | select(.Key == "_SerpData") | .Value' | python3 -c 'import json, sys; print(json.loads(sys.stdin.read() or "{}"))' | jq '.parent_collection | .object | .[]? | .id' | perl -pne 's|"(.+)"|\1|'`

### Как пострелять большим количеством контекстов сразу
Смотрите соседнюю тулзу [entity_lists_shooter](https://a.yandex-team.ru/arc/trunk/arcadia/search/wizard/entitysearch/tools/entity_lists_shooter).
