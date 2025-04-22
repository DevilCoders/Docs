# PageGate

* Родитель: [Gate](Gate.md)
* Использует: [Page](Page.md)

## API

### Свойства прототипа

#### action_loadBlocks()

`action_loadBlocks() → {Object}`

Использует [`Controller.factory`](Controller.md#factory) для создания экземпляра контроллера
страницы с текущими параметрами запроса. Выполняет рендеринг запрошенных блоков (параметр `blocks` запроса),
используя контроллер соответствующей страницы.

В случае, если результат [`Page#getAndPrepareData`](ProvidersMixin.md#getandpreparedata) имеет поле `is404` или `isServerDown`,
то вместо запрошенных блоков вызывается рендеринг `b-content` и `b-page__title`.
Если есть поле `isRedirect`, то рендерится блок `i-redirect`.

> **todo:** кажется, что не нужно прибивать это поведение гвоздями,
> но в первой итерации оставим как есть.

Возвращает объект с полем `blocks`, содержащим отрендеренные блоки:

```javascript
{
    blocks: {
        'i-redirect': '...html...',
        'b-content': '...html...',
        ...
    },

    // любое из следующих полей либо отсуствует,
    // либо содержит значение `true`
    is404: true,
    isRedirect: true,
    isServerDown: true
}
```

#### action_loadBEMJSON()

`action_loadBEMJSON() → {Object}`

> **Важно:** метод не заморожен. Его поведение может быть изменено в любом релизе,
> либо метод может быть удален. Используйте с осторожностью.

Использует [`Controller.factory`](Controller.md#factory) для создания экземпляра контроллера
страницы с текущими параметрами запроса. Выполняет рендеринг  BEMJSON запрошенных блоков (параметр `blocks` запроса),
используя контроллер соответствующей страницы.

Возвращает объект с полем `blocks`, содержащим отрендеренные блоки:

```javascript
{
    blocks: {
        'i-redirect': ...,
        'b-content': ...,
        ...
    }
}
```

Если в объекте, который является результатом [`Page#getAndPrepareData`](ProvidersMixin.md#getandpreparedata),
есть флаги `is404`, `isServerDown`, `isRedirect`, то рендеринг блоков выполняться не будет.
