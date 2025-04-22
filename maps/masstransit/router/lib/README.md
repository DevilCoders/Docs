# Формат URI

## Старый формат URI для ОТ маршрута:

Префикс: `ymapsbm1://route/transit?`

Параметры:
- `uri`: точки маршрута в формате `<x>,<y>` или `<id_остановки>`. Если между точкам нужно проехать на транспорте, то они разделены символом `>`. Если пройти пешком, то разделяющий символ - `~`. `uri` всегда заканчивается точкой прибытия в формате `<x>,<y>`.
- `avoidTypes`:  запрещенные типы транспорта через запятую в отсортированном порядке.
- `apll`: точки прибытия в формате `<x>,<y>` разделенные `~`.

Пример:
```
"ymapsbm1://route/transit?apll=~56.209630,58.005968&uri=56.223514,57.997270~stop__9906514>stop__9906330~stop__9906435>stop__9907052~56.209806,58.005691"
```

## Новый формат URI для ОТ

Префикс: `ymapsbm1://route/transit/v2?`

Параметры:
- `uri`:
    - имеет формат `<точка>~<протобуф>~<точка>~<протобуф>~...~<точка>`, где:
        - `<точка>` - это либо точка из запроса в формате `<x>,<y>`, либо id остановки.
        - `<протобуф>` - [протобуф](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/libs/uri/impl/path_uri.proto) в формате base64. В протобуфе указан тип участка маршрута и опционально подробности описываемого участка (например, промежуточные точки маршрута для пешеходных частей).
    - всегда начинается и заканчивается точками из запроса.
- `avoidTypes`:  запрещенные типы транспорта через запятую в отсортированном порядке.
- `apll`: точки прибытия в формате `<x>,<y>` разделенные `~`.

Пример (реальная длина пешеходных частей может отличаться):
```
"ymapsbm1://route/transit/v2?apll=~56.209630,58.005968&uri=53.209630,57.005968~CgoI9sK-NhCG18Q-EgUIpwEQexIGCLwEEPcIEgYI7wQQkxISBgjLBxD_DRIGCKsKEMcSEgYI3AUQ8QwSBgjgBRChChIGCJwIELUPEgYIrgUQuwoSBgjCAxDXDRIGCOcTELEOEgYI9wEQl~stop__9906330~QISBgilDBD9CBIGCMUFELcIEgYIvQEQ3QESBgi5ChCnDhIGCKEEEM~stop__9907052~RYSBgiPBRDZBhIGCJMVEPcZEgYInQMQhQISBgiTAhCtAxIGCPUBEM0BEgYI0QcQkQoSBgi5BRDXBhIGCMcJEIcMEgYInQIQ5wISBQiBARAOEgYI1wQQ0wYSBgizAxDJBBIDEI8DEgUIJRCpARIGCOkGEM0IEgYIvwQQ9QQSBgjhAxDJAhIFCB8QoA0SBgifBBCKERIGCMEKE~56.209630,58.005968"
```

## Старый формат URI пешеходных маршрутов

Префикс: `ymapsbm1://route/pedestrian?`

Параметры:
- `rll`: точки маршрута в формате `<x>,<y>`, разделенные символом `~`. **Используются только точки из запроса.**
- `apll`: точки прибытия в формате `<x>,<y>` разделенные `~`.

## Новый формат URI пешеходных маршрутов

Префикс: `ymapsbm1://route/pedestrian/v2?`

Параметры:

- `uri`:
    - имеет формат `<точка>~<протобуф>~<точка>~<протобуф>~...~<точка>`, где:
        - `<точка>` - точка из запроса в формате `<x>,<y>`.
        - `<протобуф>` - [протобуф](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/libs/uri/impl/path_uri.proto) в формате base64. В протобуфе указан тип участка маршрута и опционально подробности описываемого участка (например, промежуточные точки маршрута).
    - всегда начинается и заканчивается точками из запроса.

Пример (реальная длина протобуфа может отличаться):
```
"ymapsbm1://route/pedestrian/v2?uri=53.209630,57.005968~CgoI9sK-NhCG18Q-EgUIpwEQexIGCLwEEPcIEgYI7wQQkxISBgjLBxD_DRIGCKsKEMcSEgYI3AUQ8QwSBgjgBRChChIGCJwIELUPEgYIrgUQuwoSBgjCAxDXDRIGCOcTELEOEgYI9wEQl~56.209630,58.005968"
```
