# Contributing guide

[Как поднять начать разработку и тестирование](docs/CONTRIBUTING.md)

## Правила разработки

1. Все pull request должны быть одобрены командой сервиса и без self ship(TODO: строгие проверки)
2. Если какие-то странные тесты геопоиска покраснели - надо разобраться до коммита, можно обращаться за помощью к дежурным
3. Мы следуем [стилю кода C++ в Аркадии](https://docs.yandex-team.ru/arcadia-cpp/cpp_style_guide) и расширенному нашему стилю (ниже будет раздел с подробностями). Для python кода следуем общему стилю принятому в Аркадии
4. Форматирование кода должно производится автоматически с помощью скрипта ya style.
5. Для использования стиля в IDE нужно расширение ide для clang-format с опцией --style=file. Перед использование скопировать настройки, запустив из корня аркадии `cp devtools/ya/handlers/style/style_config .clang-format`
6. Наш проект проверяется clang-format и clang-tidy на соответствие стилю (TODO: строгие проверки)
7. Мы не уменьшаем покрытие кода тестами (ut или интегральными), за исключением отдельных случаев, которые должны быть объеснены в PR (TODO: строгие проверки)
8. Мы аккуратно работаем с добавлением зависимостей, так как это сильно влияет на скорость сборки и разработки (ознакомьтесь с 4 правилами аккуратной работы с зависимостями)

## Расширения стиля c++ кода

Строки не должны быть длинее 80-100 символов. В крайнем случае переносите длинные вызовы функций на 2 строки, но лучше порефакторить код.

### Многострочные условия для длинных проверок
Чтобы ваш файл с кодом не стал больше в ширину, чем в длину, а также чтобы избежать замыливания и стандартных ошибок в последних условиях, стоит переносить следующие операнды условия на новые строчки. Строчки следует начинать с условия

Автоформатирование не переносит строки, но не склеивает уже разбитые, которые заканчиваются операндом

сравните и найдите ошибку

``` } else if (clid == "2084802" || clid == "2084803" || clid == "2084806" || "2084807") { ```

```
}
else if(
        clid == "2084802" ||
        clid == "2084803" ||
        clid == "2084806" ||
        "2084807" // wtf????) {
```

### Пространства имен

Автоформатирвание разрешает комментарий с именем при завершении блока namespace и запрещает любые другие

namespace NNamespace {

} // namespace NNamespace

### Инициализация членов класса

Все члены класса, не имеющие конструкторов по умолчанию, всегда инициализируются при декларации (желательно с использованием оператора =, а не {})

```
class A {
        int Parameter1_ = 0; // int should be initialized
        TString Parameter2; // TString has default constructor
        bool Flag = false;
}
```

### Списки инициализации

Используйте многострочные списки инициализации для инициализации длинных массивов/структур, оставляйте , после последнего элемента, чтобы автоформатирование не пыталось склеить списки.

```
TVector<int> values = {
    1,
    2,
    3,
    4,
};
```

### Цепочки вызовов
Цепочки вызовов следует располагать многострочно, необходимо оставлять комментарий (хотя бы пустой) после каждой строчки

```
            writer->AddRow(TNode()                                                                    //
                           ("url_factors", maxUrlFactorsNode)("rubric_factors", maxRubricFactorsNode) //
                           ("geo_factors", maxGeoFactorsNode)("raw_factors", maxRawFactorsNode));
```

### Цепочки методов класса (Спеки для YT операций и др примеры)
Такие спеки предназначены для чтения только в мультистрочном режиме. 
Автоформатирование не будет их склеивать, если первая точка начата с новой строки
```
            spec.AddInput<TNode>(TRichYPath(inputTable)
                                     .Columns({PERMALINK_FIELD_NAME,
                                               IS_EXPORTED_FIELD_NAME,
                                               EXPORT_PROTO_FIELD_NAME,
                                               EXPORTED_PROTO_FIELD_NAME}))

```

```
            TReduceOperationSpec spec;
            spec.AddInput<TNode>(TRichYPath(inputTable)
                                     .Columns({PERMALINK_FIELD_NAME,
                                               IS_EXPORTED_FIELD_NAME,
                                               EXPORT_PROTO_FIELD_NAME,
                                               EXPORTED_PROTO_FIELD_NAME}))
                .AddInput<TNode>(factorsTable)
                .AddOutput<TNode>(TRichYPath(outputTable)
                                      .Schema(
                                          TTableSchema()
                                              .AddColumn("id", EValueType::VT_INT64, ESortOrder::SO_ASCENDING)
                                              .AddColumn("urls", EValueType::VT_ANY)
                                              .AddColumn("rubrics", EValueType::VT_ANY)
                                              .AddColumn("geo_id", EValueType::VT_ANY)
                                              .AddColumn("raw_factors", EValueType::VT_ANY)))
                .ReduceBy({PERMALINK_FIELD_NAME})
                .ReducerSpec(TUserJobSpec().MemoryLimit(4ULL * 1024 * 1024 * 1024));
```
