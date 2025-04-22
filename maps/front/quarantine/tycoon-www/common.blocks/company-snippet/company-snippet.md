# company-snippet

В состоянии по умолчанию отображает `company-card`, а при установке модификатора `_expanded` переключается на `company-card-with-map`.

Используется в результатах поиска и списке похожих компаний при создании организации.
В качестве данных принимает нормализованный объект компании.

```js
{
    block: 'company-card-with-map',
    company: {
        id: 42,
        names: [],
        address: {},
        emails: [],
        phones: [],
        urls: [],
        rubrics: []
    }
}
```
