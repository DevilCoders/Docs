# ControllerParams

Объект, реализующий базовые методы работы с параметрами запроса.
В [Controller](Controller.md) подмешивается к прототипу.
Можно использовать на клиенте вместе с роутером [susanin](http://github.com/nodules/susanin),
чтобы не дублировать функциональность.

## API

### getParam()

`getParam(name, defaultValue, allowedValues, allowedType) → {*}`

* `{String} name` – имя параметра;
* `{String|String[]} [defaultValue=null]` – значение по-умолчанию;
* `{String[]} [allowedValues]` – возможные значения параметра;
* `{String|RegExp} [allowedType]` – строка `"boolean"`, `"number"` или RegExp для проверки приемлемости значения.

Метод возвращает значение параметра. Если параметр не найден, то вернет `defaultValue`.

Если методу передан аргумент `allowedValues` и/или `allowedType`, то производится проверка всех значений параметра и,
если хотя бы одно из значений не удолетворяет условиям, метод вернет `defaultValue`.

### getBooleanParam()

`getBooleanParam(name, defaultValue) → {null|Boolean|Boolean[]}`

* `{String} name` — имя параметра;
* `{Null|Boolean} [defaultValue=null]` — значение по умолчанию.

Метод возвращает значение параметра, приведённое к типу `Boolean`.

### getNumericParam()

`getNumericParam(name, defaultValue, allowedValues) → {null|Number|Number[]}`

* `{String} name` — имя параметра;
* `{Null|Number} [defaultValue=null]` — значение по умолчанию;
* `{Number|Number[]} [allowedValues]` — возможные значения параметра.

Метод возвращает значение параметра, приведённое к типу `Number`.

### getParams()

`getParams(includeNames, excludeNames) → {Object}`

* `{String[]} [includeNames]` – имена параметров, которые нужно получить;
* `{String[]} [excludeNames]` — имена параметров, которые нужно исключить из результата.

Метод возвращает хэш с именами параметров в качестве ключей и значениями параметров.

Если указан массив имен параметров `includeNames`, то будут возвращены *только* параметры с именами,
входящими в этот массив. Иначе используются все параметры запроса.

Если указан массив имен `excludeNames`, то параметры с входящими в него именами *не будут* возвращены.
Аргумент `excludeNames` имеет больший приоритет, чем `includeNames`, поэтому указание имени параметра
в обоих аргументах приведет к тому, что параметр не будет возвращен.

### hasParam()

`hasParam(name, value) → {Boolean}`

* `{String} name` – имя параметра;
* `{String|String[]} [value]` – значение или массив значений параметра.

Возвращает `true` если параметр `name` передан контроллеру, иначе `false`.

Если передан аргумент `value`, то значения параметра будут проверены на соответствие значениям `value`.
В случае если параметр есть и его значения соответствуют значениям `value`, метод вернет `true`, иначе — `false`.

### hasParams()

`hasParams(names) → {Boolean}`

* `{String[]} names` — имена параметров.

Возвращает `true`, если все перечисленные параметры переданы контроллеру.

