# TemplateMixin

## API

### Статические свойства

#### TemplateError

Класс ошибок `TemplateError`, наследник [`AbstractControllerError`](AbstractControllerError.md).

Коды ошибок:

* `METHOD_NOT_IMPLEMENTED` – абстракный метод `TemplateMixin` не реализован в классе, к которому подмешан миксин.

### Свойства прототипа

#### prepareData()


`prepareData(data) → {Object}`

* `{Object} [data]` — объект с данными и хэлперами.

Возвращает расширенную дополнительными свойствами shallow-копию объекта `data`.

Дополнительные свойства:

* `{Function} getPageParam` — [`Controller.getParam()`](ControllerParams.md#getparam);
* `{Function} getPageParams` — [`Controller.getParams()`](ControllerParams.md#getparams);
* `{Function} hasPageParam` — [`Controller.hasParam()`](ControllerParams.md#hasparam);
* `{String} pageType` — [`Controller#type`](Controller.md#factory);
* `{Function} extend` — [`util.extend()`](https://github.yandex-team.ru/pages/nodules/libs/myUtil.html#extend);
* `{Debug} debug` — [`Debug`](https://github.yandex-team.ru/pages/nodules/libs/Debug.html).

#### getHTML()

> Абстрактный метод

`getHTML(block, data, dataForBlock) → {String}`

* `{String} block` — имя блока, который нужно отрендерить;
* `{Object} [data]` — данные и хэлперы, `prepareData` будет применен к этому объекту;
* `{Array} [dataForBlock]` – массив аргументов для вызова метода блока.

См. пример реализации в [`BEMTemplateMixin`](BEMTemplateMixin.md).
