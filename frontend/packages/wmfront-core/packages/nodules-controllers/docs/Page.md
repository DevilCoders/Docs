# Page

Базовый контроллер страницы.

* Родитель: [Controller](Controller.md)
* Подмешаны: [ProvidersMixin](ProvidersMixin.md), [TemplateMixin](TemplateMixin.md)

## API

### Статические свойства

#### action()

`action(descriptor) → Page`

* `{Object} action` – описание действия
  * `{String} action.name` – имя; конечное имя метода: `action_<action.name>`;
  * `{String|String[]} [action.blocks]` –  блок или массив блоков для которых будет вызыватся `getData()`, и которые будут по-умолчанию добавлены в список блоков для рендеринга;
  * `{Boolean} [action.render]` – необходимо ли после выполнения действия выполнить рендеринг блоков;
  * `{Function} action.fn` – функция, которая будет добавлена в цепочку промисов после `getAndProcessData()`.

Если выставлен флаг `action.render`, то:

* `action.fn` должна вернуть хэш `data` или промис, оторый резолвится с `data`;
* в `action.fn` доступен массив блоков для последующего рендеринга в поле `data.renderBlocks`, который можно изменять.

### Свойства прототипа

#### getAndProcessData()

`getAndProcessData([blocks], [action]) → {Promise}`

* `{String|String[]} [blocks]` — передается внутри метода в [`ProvidersMixin#getData`](ProvidersMixin.md#getdata).
* `{String} [action]` — передается внутри метода в [`ProvidersMixin#getData`](ProvidersMixin.md#getdata).

Метод возвращает промис.

Отмененный промис [`Controller#getData`](ProvidersMixin.md#getdata) обрабатывается внутри метода.
Метод `getAndProcessData` всегда разрешает промис.

Ошибки [`Controller#getData`](ProvidersMixin#getdata) проверяются на наличие следующих полей:

* `error.is404` — объект `data` подменяется на `{ is404: true, pageType: '404' }`;
* `error.redirect` — объект `data` подменяется на
`{ isRedirect: true, isRealRedirect: error.isRealRedirect, redirectTo: error.redirect }`

Если ни одно из вышеперчисленных полей не определено, то объект подменяется на следующий:

```javascript
{
    isServerDown: true,
    pageType: 'server-down'
}
```

После чего логируется ошибка контроллера и промис разрешается подмененным объектом для рендеринга страницы об ошибке.
