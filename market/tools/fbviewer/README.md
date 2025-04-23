# Программа для показа содержимого файлов на flat buffers в "человекочитаемом" виде

## Краткое описание
1. Программа берет на вход файл на flat buffers и пытается вывести его в человекочитаемом виде.
2. Пока есть только один формата вывода: json.
3. Если не задан конкретный парсер файла (--type), то пытаемся выбрать из существующих тот, который сможет провалидировать входной документ.
4. Список всех доступных парсеров можно посмотреть через ключ --list.
5. Можно просто провалидировать файл и узнать его сигнатуру через ключ --validate.
6. Можно сконвертировать json в flatbuffers файл --fb-from-json (будет полезно для тестов).
7. Можно вывести схему из ресурсов, чтобы проверить ее актуальность (опция --print-schema).


## Пример использования
1. Список возможных опций

```
a-anikina@qtest-virt02ht:/usr/lib/yandex$ ./fbviewer --help
Prints .fb file in human-readable view and converts json files to fb files

Usage: ./fbviewer [OPTIONS] [Input] [Output]

Options:
  {-V|--svnrevision} print svn version
  {-?|--help}        print usage
  --format VAL       output format: json (default: "json")
  --type VAL         input file's format, auto or file's type name (default: "auto")

  --list             option to list all possible types of viewers (default: 0)
  --validate         just validate file and get it's signature (default: 0)
  --fb-from-json     convert json file to fb (default: 0)
  --print-schema     print fb schema (default: 0)
```

Free args: min: 0, max: 2 (listed described args only)
  Input   File to parse. It could be *.fb file or *.json file for --fb-from-json option
  Output  Output file

2. Вывести конктерный файл в json формате
```
a-anikina@qtest-virt02ht:/var/lib/yandex/indexer/market/mif/offers/20181212_1342-0/workindex$ /usr/lib/yandex/fbviewer base-offer-props.fb

{
  "BaseProperties": [
    {
      "Price": 0,
      "CurrencyId": 3,
      "Flags32": 0,
      "HistoryPrice": {
        "Value": 11600000000
      },
      "HistoryCurrencyId": 3,
      "EnableAutoDiscounts": false,
      "HistoryPriceIsValid": true
    },
    {
      "Price": 0,
      "CurrencyId": 3,
      "Flags32": 0,
      "HistoryCurrencyId": 3,
      "EnableAutoDiscounts": true,
      "HistoryPriceIsValid": false
    }
  ]
}
```

4. Узнать о всех доступных парсерах

```
a-anikina@qtest-virt02ht:/usr/lib/yandex$ ./fbviewer --list
DeliveryModifierVecViewer
TAmoreDataVecViewer
TBasePropertiesExtViewer
TBasePropertiesViewer
...
```

5. Провалидировать файл и узнать его сигнатуру

```
a-anikina@qtest-virt02ht:/var/lib/yandex/indexer/market/mif/offers/20181212_1342-0/workindex$ /usr/lib/yandex/fbviewer some_wrong_file.txt --validate
There is no suitable viewer in fbviewer tool (to see all implemented types type list option (--list) or file is invalid

a-anikina@qtest-virt02ht:/var/lib/yandex/indexer/market/mif/offers/20181212_1342-0/workindex$ /usr/lib/yandex/fbviewer base-offer-props.fb --validate
TBaseOfferPropsViewer
```

6. Сконвертировать json файл в fb.

```a-anikina@dev-idx01vd:~/arcadia/market/tools/fbviewer$ ./fbviewer base-offer-props.json base-offer-props-test.fb --fb-from-json --type TBaseOfferPropsViewer```

7. Вывести схему fb файла из ресурсов

```a-anikina@dev-idx01vd:~/arcadia/market/tools/fbviewer$ ./fbviewer --print-schema --type TBaseOfferPropsViewer```

## Как добавить новый формат?
1. Добавить fb-схемы в ресурсы src/ya.make
2. Добавить валидатор в библиотеку flat_helpers.
3. Воспользоваться макросом FBVIEWER, передать имена всех fb-схем необходимых для парсинга в виде пар {путь к схеме в системе ресурсов; имя, под которым она используется в include}.
Важно! Сначала нужно добавлять те схемы, которые используются как инклуды. Если попробовать парсить какую-то схему до того, как пропарсили ее инклуд, то произойдет ошибка.
4. Добавить тип новый вьюер в TViewers TFBViewerStorage::MakeViewersList().


## Планы по доработке (a-anikina)
1. Добавить опцию вывода конкретного документа по его номеру
2. Вывод в plain формате (если будут запросы на него).
