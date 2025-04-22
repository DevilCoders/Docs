Парсит cgi-параметры в протобуф.

Делает валидацию всех параметров:
* Проверка типов
* Проверка required
* Проверка repeated (если поле не repeated, то не больше одного значения)
* Проверка значений enum

Пример:

* протобуф:
```
message TExampleSimple {
    optional string OptionalParam = 1 [(NBSYeti.QueryParameterName) = "opt"];
    required uint64 RequiredParam = 2 [(NBSYeti.QueryParameterName) = "required"];
    repeated string RepeatedParam = 3 [(NBSYeti.QueryParameterName) = "multiple"];
}
```

* парсинг:

```
auto proto = ParseQueryArgsToProto<TExampleSimple>(TCgiParameters{"required=42&opt=A&multiple=1&multiple=2"});
```

* результат:

```
{
    "OptionalParam": "A",
    "RequiredParam": 42,
    "RepeatedParam": ["1", "2"]
}
```

Производительность. Эта библиотека не ориентирована на производительность,
но тем не менее работает достаточно быстро.

```
enum=opt14&i32=10032&i64=10064&ui32=20032&ui64=20064&double=0.25&float=0.5&str=abacaba&bool=1&enum_r=opt14&enum_r=opt13&enum_r=opt12&i32_r=10032&i64_r=10064&ui32_r=20032&ui64_r=20064&double_r=0.25&float_r=0.5&str_r=abacaba&bool_r=0"
```

Вот такие параметры парсятся по протобуфной схеме с 18 полями
(в том числе двумя enum с 14 значениями)
за 4-5 микросекунд.
