## Storage API {#storage-api}

Все ручки поддерживают только метод GET.

### /storage/shards
Перечислить шарды (здесь — кортежи `(project; service)`):

Агент отвечает в формате JSON. Пример:

```json
[{"project":"test-project","service":"test-service"},{"project":"test-project","service":"sys"}]
```

## /storage/*

{% note warning %}

Для следующих ручек обязательны параметры `project` и `service`, а также заголовок `X-Solomon-FetcherId` (подробнее про этот заголовок ниже).
Без них агент вернет 400.

{% endnote %}

В целом find и read работают одинаково, но find возвращает только метки без точек.

Формат ответа определяется либо параметром `?format=JSON` / `?format=SPACK`, либо заголовком `Accept` со значениями `application/json`/`application/x-solomon-spack`. Если заданы оба, приоритет будет у GET-параметра `format`.

### /storage/find
Перечислить метки, соответствующие заданному условию. Для фильтрации можно задать параметры `matchType` и `labels`. Поддерживаемые matchType [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/solomon/agent/misc/labels_match.h)

Пример:
```bash
curl "localhost:8088/storage/find?project=test-project&service=sys&matchType=EXACT&labels=mountpoint=/&pretty=true" -H "X-Solomon-FetcherId: foo"
```

Ответ:
```json
{
    "sensors":[
        {
            "kind":"GAUGE",
            "labels": {
                "mountpoint": "/",
                "path": "/Filesystem/SizeB"
            }
        },
        {
            "kind": "GAUGE",
            "labels": {
                "mountpoint": "/",
                "path": "/Filesystem/UsedB"
            }
        },
        {
            "kind": "GAUGE",
            "labels": {
                "mountpoint": "/",
                "path": "/Filesystem/FreeB"
            }
        }
    ]
}
```

### /storage/read

Поскольку кластеров, которые приходят за данными может быть несколько, а отдавать одни и те же данные мы хотим каждому из них только по одному разу, агент поддерживает отступы для всех известных ему fetcher'ов, которые идентифицируют себя заголовком `X-Solomon-FetcherId`.

При запросе на чтение агент отдает дополнительные заголовки `X-Solomon-HasMore` и `X-Solomon-NextSequenceNumber`:

```
curl "localhost:8088/storage/read?project=test-project&service=sys&matchType=EXACT&labels=mountpoint=/&pretty=true" -H "X-Solomon-FetcherId: foo" -v
...
< X-Solomon-HasMore: 0
< X-Solomon-NextSequenceNumber: 169
```

`X-Solomon-HasMore` говорит fetcher'у, что у агента есть больше данных, которые соответствуют запросу на чтение, но не вошли в лимит. Т.е fetcher'у можно не ждать таймаута на опрос этого агента, а делать запрос сразу.

`X-Solomon-NextSequenceNumber` это отступ, который fetcher'у следует выставить в заголовке `X-Solomon-SequenceNumber` в следующем запросе, чтобы читать только новые данные. Если этот заголовок не будет выставлен, fetcher будет получать самые старые данные, которые есть у агента, потому что запись отступа прочитанного происходит только в момент **следующего** запроса с заголовком `X-Solomon-SequenceNumber`. Только таким образом агент может убедиться, что предыдущая порция данных обработана Соломоном.

Текущая логика работы в зависимости от значения отступа: [блок-схема](https://jing.yandex-team.ru/files/ivanzhukov/agent_storage_offsets_logic.png)

### /storage/readAll
TODO(ivanzhukov@)

## Management API {#management-api}
Если в конфиге задана секция `ManagementServer`, то агент также стартует сервер с собственными сенсорами и отладочной информацией на отдельном порту.

### /counters
отдает внутренние метрики работы Агента

* /counters
* /counters/json
* /counters/spack

### /modules
отдает список загруженных модулей и информацию про них

* /modules
* /modules/json
