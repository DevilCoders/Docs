# Releases Monitoring

Тул `releases_monitoring` запускается по крону каждый день в 21-00 и проверяет, выкатились ли свежие данные в продакшен. Если нет - создаёт отчёт в тикете в очереди MAPSLSR.

Если тул падает, это не является критической поломкой. Чинить тул ночью и в выходные нет необходимости.

Конфигурация проверки задаётся в `module_traits.json` и в server-конфиге шедьюлера в секции `releases_monitorings`.

Пример server-конфига шедьюлера:
```json
"releases_monitorings": [
    {
        "contour": "stable",
        "startrek_queue": "MAPSLSR"
    },
    {
        "contour": "datatesting",
        "startrek_queue": "MAPSGARDEN"
    }
]
```

В `module_traits.json` используются опции:
- `track_ancestors_from`: проверяется свежесть исходных данных только по соответствующему пути в графе
- `freshness_check`: в поле `source` перечисляются source-модули, свежесть используемых билдов которых нужно проверять.
Предполагается, что это `ymapsdf_src` или `mtr_mpro_export_src`

```json
"freshness_check": {
    "sources": ["ymapsdf_src"]
}
```
