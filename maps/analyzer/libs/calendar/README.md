Библиотека для работы с календарем праздничных дней
===

В библиотеке описаны основные типы для работы с календарем: создания и чтения информации о рабочих и выходных днях

Основные хэдеры:
- [`calendar.h`](include/calendar.h) – описывает информацию о "локальной дате" (страна + местная дата с учетом временной зоны)

Директория /fb библиотеки описывает процесс сериализации и десериализации во flatbuffer:
- [`builder.h`](include/fb/builder.h) – описание типов, необходимых для сериализации данных и записи в файл
- [`common.h`](include/fb/common.h) – описание типов, необходимых для использования во внутренней реализации `unordered map`
- [`map_builder.h`](include/fb/map_builder.h) – реализация сериализации `unordered map` во `flatbuffer`
- [`map_reader.h`](include/fb/map_reader.h) – реализация десериализации `unordered map` из `flatbuffer`
- [`reader.h`](include/fb/reader.h) – описание типов, необходимых для чтения и десериализации данных
- [`storage.fbs64`](impl/fb/storage.fbs64) – схема данных flatbuffer64

Пример использования:
===
```cpp
const std::string FB_PATH = ...
const auto GEOBASE_BIN_PATH = ...
const auto TZDATA_PATH = ...

const NGeobase::TLookup geobase(
    NGeobase::TLookup::TInitTraits()
        .Datafile(GEOBASE_BIN_PATH)
        .TzDataPath(TZDATA_PATH)
);

const auto cal = calendar::loadCalendar(FB_PATH);

time_t timestamp = ...
maps::geolib3::Point2 point = ...
const auto localDate = calendar::getLocalDate(
    timestamp, point, geobase
);

if (cal.getDateInfo(localDate).isHoliday) {
    std::cout << "It's time to relax" << std::endl;
} else {
    std::cout << "It's time to work" << std::endl;
}

return 0;
```

Пример создания данных:
===
```cpp
namespace calendar = maps::analyzer::calendar;

int main(int argc, char* argv[])
{
    maps::cmdline::Parser parser;

    const auto files = parser.strings("files").help("source xml files").required();
    const auto outputPath = parser.string("output").help("output file path").required();
    const auto version = parser.string("version").help("version to be written").required();

    parser.parse(argc, argv);

    calendar::flat_buffers::CalendarStorageBuilder builder {
        version,
        files.size()
    };

    for (const auto& file: files) {
        const NXml::TDocument xml{TString{file}, NXml::TDocument::File};
        calendar::tools::processXml(xml, &builder);
    }

    builder.flushToFile(outputPath);

    return 0;
}
```

Далее подобный исполняемый файл можно будет использовать для создания сериализованных данных из xml-файлов, полученных от API календаря:
```bash
./builder --files region255.xml --files region149.xml --version test --output calendar.fb
```

Описание сериализации unordered map:
===
Для использования в календаре была реализована обобщенная схема создания, сериализации и десериализации `unordered map` с произвольными типами ключа и значения.
Тип ключа / значения может быть:
– скалярной величиной
– составным типом / собственной структурой

Для собственных структур необходимо определить классы `KeyReader` / `KeyWriter` / `ValueReader` / `ValueWriter`. Writer'ы должны конструироваться из значения, иметь конструктор по-умолчанию и метод `commit`, принимающий `flatbuffers64::FlatBufferBuilder*` и возвращающий `Offset`. Reader'ы должны конструироваться из указателя на flatbuffer-ную структуру данных. Также необходимо в схеме создать обертки для ключа и значения, которые содержат поле `value` желаемого типа и, для скалярных типов, `isNull: bool`. Затем, необходимо описать структуру, содержащую массив ключей (оберток) с именем `hashTableKeys` и массив значений (оберток) с именем `hashTableValues`. Пример:
```proto
table NonScalarData {
    foo: ulong;
    bar: string;
}

table KeyPtr {
    value: ulong;
    isNull: bool;
}

table ValuePtr {
    value: NonScalarData;
}

table Map {
    hashTableKeys: [KeyPtr];
    hashTableValues: [ValuePtr];
}
```
Имена структур произвольные, но сгенерированные для них builder'ы, как, собственно, и тип builder'а для самой структуры мапы в схеме, надо будет указать в качестве параметров шаблона для метода `commit` у класса `MapWriter`. Пример:
```cpp
struct MyStorageWriter {
    ...
    auto MyStorageWriter::commit(
        flatbuffers64::FlatBufferBuilder* builder
    ) const {
        const auto myMapOffset = mapWriter_.commit<
            fbs64::KeyPtrBuilder,
            fbs64::ValuePtrBuilder,
            fbs64::MapBuilder
        >(builder);

        return fbs64::CreateMyStorage(
            *builder,
            regionMapOffset
        );
    }
    ...
    MapReader<uint64_t, NonScalarDataReader, fbs64::Map> mapWriter_;
}
```
`KeyReader` и `KeyWriter` должны быть сравнимы (`operator!=`) с соответствующими данными, которые они читают / пишут (т.е. данными типа ключа).
