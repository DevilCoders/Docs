# Описание параметра `conditions`

Элементарное (единичное, простое) Условие, в общем случае, состоит из трех элементов: Поля, Предиката и Образца.

- *Поле* _(field)_ - "что сравниваем", какое-то свойство письма, которое требуется проверить.
- *Предикат* _(matcher)_ - "как сравниваем", операция сравнения (равно, не равно, содержит, существует и т.п.)
- *Образец* _(pattern)_ - "с чем сравниваем", строка-образец с которой осуществляется сравнение выбранного поля.

| Запись условия | Описание | Примеры |
|----------------|----------|---------|
| ```{ "field": "value" }``` | Значение поля field  равно value | ```{ "address:from": "friend@mail.ru" }```<br/>```{ "attach:filename": "Квитанция.pdf" }``` |
| ```{ "field": [ "value1", "value2", ... ] }``` | Значение поля field  равно или value1 , или value2  и т.д. | ```{ "from": [ "Alice", "Bob" ] }``` |
| ```{ "field": { "operation": "value" } }``` | Значение поля field  сравнивается со значением value  с помощью операции operation | ```{ "subject": { "$contains": "выигрыш" } }```<br/>```{ "header:return-path": { "$not-contains": "@gmail.com" } }``` |
| ```{ "field": { "$base64": "dmFsdWU=" } }``` | Значение поля field  равно value , записанному в формате base64 | ```{ "address:from": { "$base64": "ZnJpZW5kQG1haWwucnU=" } }``` |
| ```{ "field": { "$exists": true/false } }``` | Поле field  существует /не существует  (имеет смысл для проверки заголовков) | ```{ "header:return-path": { "$exists": true } }```<br/>```{ "header:x-yandex-forward": { "$exists": false } }``` |
| ```{ "field": { "operation": { "group": [ "value1", { "$base64": "dmFsdWUy" }, ...  ] } } }``` | Поле field  проверяется в соответствии с operation  с группой group  значений value1 , value2  (задано в base64) и т.д. | ```{ "subject": { "$contains": { "$any": [ "hello", "bye" ] } } }```<br/>```{ "body": { "$not-contains": { "$all": [ { "$base64": "0J/RgNC40LLQtdGC" }, { "$base64": "0J/QvtC60LA=" } ] } }``` |

_Составные (сложные)_ Условия могут быть образованы из других условий, как простых так и сложных, с помощью объединения их в логические группы по "И" (все должны быть выполнены) или по "ИЛИ" (достаточно выполнения хотя бы одного).

| Запись условия | Описание | Примеры |
|----------------|----------|---------|
| ```{ "field1": "value1", "field2": { "operation": "value2" } }``` | Значение поля `field1` равно `value1`, *И* при этом значение `field2` соответсвует `value2` (согласно предикату `operation`) | ```{ "from": "friend@mail.ru", "attach:filename": "Квитанция.pdf" } |
| ```{ "logic-operation": [ { "field1": "value1" }, { "field2": { "operation": "value2" } } ]}``` | Условия:<br/>- значение поля `field1` равно `value1`<br/>- значение `field2` соответсвует `value2` (согласно предикату `operation`)<br/>объединены в соответствии с `logic-operation` (*И* или *ИЛИ*) | ```{ "$and": [ { "from": "friend@mail.ru" }, { "attach:filename": "Квитанция.pdf" }]}```<br/>```{ "$or": [ { "from": "friend@mail.ru" }, { "attach:filename": "Квитанция.pdf" }]}``` |

## Поле

Полное название поля формируется из _названия группы_ (если присутствует) и _названия поля_ разделенных символом `:`  - `"группа:поле"` или `"поле"`. Некоторые группы, например `address`, могут быть опущены, а некоторые, например `header`, обязательны.

Множество допустимых полей

| Группа  | Поле | Описание | Примеры |
|---------|------|----------|---------|
| address | from<br/>to<br/>cc<br/>tocc | _email_ или _display-name_<br/>- отправителя<br/>- получателя<br/>- получателя копии<br/>- получателя или получателя копии | `address:from`<br/>`from`<br/>`address:to`<br/>...<br/>`address:tocc`<br/>`tocc` |
|         | subject | _Тема_ письма | `subject` |
| header  | произвольная строка | Заголовок письма | `header:x-yandex-spam`<br/>`header:return-path`<br/>... |
|         | body | Тело письма | `body` |
| attach  | filename | Название файла-вложения | `attach:filename` |

## Предикат

| Предикат | Описание |
|----------|----------|
| $eq | Совпадает, равно |
| $ne | Не совпадает, не равно |
| $contains | Содержит |
| $not-contains | Не содержит |
| $exists | Существует (не существует) |

## Образец

_Образец_ обычно представляет строку для сравнения заданным способом с содержимым некоторого поля. Если образец трудно представить непосредственно в виде строки, то можно передать его в закодированном виде, base64.

| Запись условия | Описание | Примеры |
|----------------|----------|---------|
| ```{ "field": { "$base64": "dmFsdWU=" } }``` | Значение поля field  равно value , записанному в формате base64 | ```{ "address:from": { "$base64": "ZnJpZW5kQG1haWwucnU=" } }``` |


{% cut "Пример 1: 'От кого' совпадает c 'hello@ya.ru'" %}

`address:from=="hello@ya.ru"`
```json
{ "address:from": "hello@ya.ru" }
```

{% endcut %}

{% cut "Пример 2: 'От кого' совпадает c 'hello@ya.ru' (задано в base64)" %}

`address:from=="fromBase64('aGVsbG9AeWEucnU=')"`
```json
{ "from": { "$base64": "aGVsbG9AeWEucnU=" } }
```

{% endcut %}

{% cut "Пример 3: 'От кого' содержит '@yandex.ru' И в теме письма есть 'hello' ИЛИ 'bye'" %}

`address:from=="%@yandex.ru%" AND (header:subject=="%hello%" OR header:subject=="%bye%")`
```json
{
    "address:from": { "$contains": "@yandex.ru" },
    "subject": { "$contains": [ "hello", "bye" ] }
}
```

или

```json
{
    "$and": [
        { "address:from": { "$contains": "@yandex.ru" } },
        { "subject": { "$contains": { "$any": [ "hello", "bye" ] } } }
    ]
}
```

или

```json
{
    "$and": [
        { "address:from": { "$contains": "@yandex.ru" } },
        { "$or": [ {"subject": { "$contains": "hello" } }, { "subject": { "$contains": "bye"} } ] }
    ]
}
```

{% endcut %}

{% cut "Пример 4: Присутствует заголовок 'x-yandex-spam'" %}

`header:x-spam-flag EXISTS`

```json
{ "header:x-spam-flag": { "$exists": true } }
```

{% endcut %}

{% cut "Пример 5: Для заголовока 'x-yandex-spam' задано значение 'yes'" %}

`header:x-spam-flag=="yes"`

```json
{ "header:x-spam-flag": "yes" }
```

{% endcut %}

{% cut "Пример 6: Для заголовока 'x-yandex-spam' задано значение отличное от 'yes'" %}

`header:x-spam-flag!="yes"`

```json
{ "header:x-spam-flag": { "$ne": "yes" } }
```

{% endcut %}

## Грамматика описания условий

```
%start
    : CONDITION

CONDITION
    : {}
    | { CONDITION_PAIR, ... }

CONDITION_PAIR
    : KEY: COMPARISON
    | HEADER_KEY: EXIST_VALUE
    | "$and": [ CONDITION, ... ]
    | "$or":  [ CONDITION, ... ]

COMPARISON
    : VALUE
    | VALUE_LIST
    | { OP: VALUE }
    | { OP: VALUE_LIST }

KEY
    : "address:from" | "address:to" | "address:cc" | "address:tocc" | "from" | "to" | "cc" | "tocc"
    | "subject"
    | "body"
    | "attach:filename"
    | HEADER_KEY

HEADER_KEY
    : "header:HEADER_NAME"

OP
    : "$eq"
    | "$ne"
    | "$contains"
    | "$not-contains"

VALUE
    :  STRING
    | { "$base64": STRING }

VALUE_LIST
    : [ VALUE, ... ]
    | { "$any": [ VALUE, ... ] }
    | { "$all": [ VALUE, ... ] }

EXIST_VALUE
    : { "$exists": BOOLEAN }

HEADER_NAME
    : [-_a-zA-Z0-9]+

STRING
    : ".*"

BOOLEAN
    : true
    | false
```
