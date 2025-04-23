Каждый YT-логгер имеет свою категорию, и создается таким образом:
```c++
::NYT::NLogging::TLogger logger1("CATEGORY");
```

Инициализация правил проходит после вызова функции и передачи ей protobuf-сообщения с правилами логгирования:
```c++
NYTEx::NLogging::Initialize(config);
```

В конфигурации вы можете определить набор правил логгирования. Каждое правило позволяет направить логи по категориям и уровням логгирования в разные файлы.

Значения по умолчанию можно увидеть в "ads/bsyeti/libs/ytex/logging/proto/config.proto". Если не будут указаны IncludeCategories или ExcludeCategories, то по умолчанию будут включены все категории. В случае отсутсвия хоть одного правила, все логи будут направлены в stderr. В случае если категория не попадает не под одно правило, то ее лог не записывается. Поле ExcludeCategories не учитывается если уже указано правило IncludeCategories

Пример:
```json
{
    // Допустим у нас есть три логгера с категориями "A", "B" и "C"
    "Rules": [
        {
            // В файл "AB.log" попадут категории "A" и "B" с диапозоном уровней [DEBUG:ERROR]
            "FilePath": "AB.log",
            "MinLevel": "Debug",
            "MaxLevel": "Error",
            "IncludeCategories": ["A", "B"]
        },
        {
            // В файл "AC.log" попадут все категории кроме "B" (А и С) c диапозоном уровней [WARN:MAX)
            "FilePath": "AC.log",
            "MinLevel": "Warning",
            "ExcludeCaregories": ["B"]
        }
    ]
}
```

Доступные уровни логгирования:
- Minimum
- Trace
- Debug
- Info
- Warning
- Error
- Alert
- Fatal
- Maximum


Для интеграции с другими библиотеками логирования смотри [adapters](adapters/).
