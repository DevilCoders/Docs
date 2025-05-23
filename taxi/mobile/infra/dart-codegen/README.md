# dart-codegen

KN утилита для генерации Dart метрик по .yaml файлам.

Собирается под MacOs, Linux, Jvm.

Запускаем бинарник/джарник с передачей параметров

```shell
-s path/to/file.yaml
-o directory/for/generate/code
-v true/false
```
`-s (обязательный)` - путь к файлу со спекой аналитики

`-o (обязательный)` - путь к директории куда будет генериться код

`-v (не обязательный)` - надо ли включать валидацию. По умолчанию true.
Валидация проверят типы `object`, что среду полей `type` в событиях и праметрах нет левых типов, только те, что перечислены в спеке.

Полная команда запуска выглядит так:

```shell
dart-codegen -s metrica.yaml -o models/ ; dart format ../lib/metrica/models/
```

`dart format` стоит добавить для красивого форматирования вашего кода.

## Формат yaml файла

Формат описан в файле example.yaml.

| Поддерживаемые типы |
|:--------------------|
| int                 |
| float               |
| string              |
| boolean             |
| list                |
| map                 |
| object(param)       |

Список типизируется одним из поддерживаемых примитивов (или object).
В словаре указывается 2 типа. `map<типключа,типзначения>`.
object - это тип параметра, то есть можно внутри 1 параметра юзать другой, также его можно юзать в списках и словарях.

Для нуллабл значений на конце указывается вопросительный знак `string?`.
