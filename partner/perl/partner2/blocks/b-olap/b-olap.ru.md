Контролы блока вынесены в отдельный блок `b-olap-controls`. Внутри блока есть реализация источника данных `DataSource`. Для корректной работы в блок необходимо отдать метаданные в виде:
```
{
    "dim_names": { "dimId": "dimName", ... , ""dimId: "dimName" },
    "metric": "metricName",
    "dim_order": [ "dimId", ... , "dimId" ],
    "dimensions": {
        "dimId": {
            "label": "dimName",
            "type": "dictionary",
            "values": [
                {"label": "Value name", "id": 0},
                ...
                {"label": "Value name", "id": 1},
            ]
        },
        "dimID": {"label": "dimName", "type": "date"}
    },
    "calendar": "calendarDim"
}
```

Методы
======
- `_createDataSource` Создает источник данных `DataSource`
- `_buildTable` Генерирует html таблицы `b-table`
- `_buildChart` Генерирует html диаграммы `b-chart`
- `_buildExport` Изменяет данные `b-export`
- `setData` Устанавливает данные в `DataSource`
- `hasData` Возвращает флаг наличия данных в `DataSource`
- `clearData` Очищает данные в `DataSource`
- `setFilters` Устанавливает фильтры в `DataSource`. Используются фильтры, возвращаемые из метода getConfig() у b-simple-search
- `setGroupBy` Устанавливает группировку по измерениям в `DataSource`
- `buildResults` Строит элементы блока: диаграмму, таблицу и экспорт в соответствии с текущим состоянием `DataSource`
