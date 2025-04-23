# Инструмент анализа распределения занимаемого места внутренними структурами данных в файле flatbuffer

## Запуск
```bash
ya make . -r && ./introspect /path/to/calendar.fb
```

## Пример результата
```
maps.analyzer.calendar.flat_buffers.fbs64.Calendar: 3.68 Kb {
    regionMap: 2.25 Kb {
        hashTableKeys: 356 b {
            value: 160 b;
            isNull: 20 b;
        };
        hashTableValues.value: 1.90 Kb {
            rangeStart: 16 b;
            values: 1.71 Kb {
                dateType: 62 b;
                isHoliday: 62 b;
                isTransfer: 62 b;
                holidayName: 1.01 Kb;
            };
        };
    };
    version = "test": 4 b;
};
```
