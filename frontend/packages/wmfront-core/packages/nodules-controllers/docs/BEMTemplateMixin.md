# BEMTemplateMixin

## Пример

```javascript
MyController.mixin(BEMTemplateMixin, './priv.js', false);
```

## API

### Статические свойства

#### BEMTemplateError

Класс ошибок `BEMTemplateError`, наследник [`TemplateMixin.TemplateError`](TemplateMixin.md#templateerror).

Коды ошибок:

* `PRIV_EXECUTION_FAILED` — ошибка возникает при подключении priv.js файла (например, при наличии синтаксических ошибок);
* `BLOCK_EXECUTION_FAILED` — ошибка при выполнении функции блока;
* `BEMHTML_NOT_DEFINED` — priv.js не экспортирует функцию `BEMHTML()`;
* `BEMHTML_APPLY_ERROR` — ошибка при выполнении функции `BEMHTML()` к BEMJSON–объекту блока;
* `BLOCKS_NOT_DEFINED` — priv.js не экспортирует хэш `blocks`

#### setPriv()

`setPriv(pathToPriv, debug) → this`

* `{String} pathToPriv` — путь до priv-файла шаблона;
* `{Boolean} [debug=false]` — режим отладки

Необходимо помнить, что непосредственно подключение priv.js и оборачивание блоков производится один раз для одного файла,
поэтому если первый раз в приложении priv.js был подключен с флагом `debug=true`, то при всех последующих вызовах
будет использоваться уже обернутая версия с отладочным выводом. Верно и обратное.

Может бросить ошибку [`BEMTemplateError`](bemtemplateerror) с кодами `PRIV_EXECUTION_FAILED`, `BEMHTML_NOT_DEFINED` и `BLOCKS_NOT_DEFINED`.

Возвращает `this`.

### Свойства прототипа

#### setPriv()

См. описание статической версии метода [`setPriv()`](#setpriv). Разница в том, что вызов статического метода устанавливает
priv в прототипе конструктора, а метод прототипа — в инстансе.

#### getHTML()

Реализация [`TemplateMixin#getHTML()`](TemplateMixin.md#gethtml).

`getHTML(block, data, dataForBlock) → {String}`

* `{String} block` — имя блока, который нужно отрендерить;
* `{Object} [data]` — данные и хэлперы, `prepareData` будет применен к этому объекту;
* `{Array} [dataForBlock]` – массив аргументов для вызова метода блока.

Возвращает строку HTML, если внутренний вызов [`getBEMJSON`](#getbemjson) вернул `null`.

Если вызов функции `BEMHTML()` из priv.js привел к ошибке, то вернет пустую строку
и залогирует ошибку [`BEMTemplateError`](#bemtemplateerror) с кодом `BEMHTML_APPLY_ERROR`.

#### getBEMJSON()

`getBEMJSON(block, data, dataForBlock) → {*}`

* `{String} block` — имя блока, который нужно отрендерить;
* `{Object} [data]` — данные и хэлперы, `prepareData` будет применен к этому объекту;
* `{Array} [dataForBlock]` – массив аргументов для вызова метода блока.

Вызывает обернутый метод блока `block` из priv-файла. Перед этим priv'у устанавливается объект данных `data`.
Массив `dataForBlock` используется, как набор аргументов для метода блока.

Если блок не определен или не найден в priv-файле, то метод вернет `null`, иначе — результат выполнения метода блока.

Если вызов функции блока привел к ошибке, то вернет пустую строку (или строку с описанием ошибки в режиме отладки) и 
залогирует ошибку [`BEMTemplateError`](#bemtemplateerror) с кодом `BLOCK_EXECUTION_FAILED`.
