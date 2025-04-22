r103821
# Блок фильтра для простого поиска по тексту.

Представляет собой блок, содержащий поле ввода для фильтрации по какому либо DOM элементу.

Например, это может быть блок селекта, который "умеет" работать с интерфейсом i-handle-filter

Пример:

```javascript
{
    block: 'select',
    mods: { size: 's', theme: 'normal', type: 'with-filters' },
    content: [
        { block: 'button', mods: { size: 's' } },
        {
            elem: 'filters',
            filter: {
                block: 'b-simple-text-filter',
                // опционально включается поиск и по ключу хэша (в данном случае это id)
                filterByKey: true,
                // простой хэш ключ:текст, по которому будет производиться поиск
                hashMap: [{ id: 1, text: 'hello' }].reduce(function(hash, item) {
                    hash[item.id] = item.text;

                    return hash;
                }, {}),
                // хинт-текст для пустого поля ввода
                hint: iget('Найти')
            }
        },
        {
            elem: 'control',
            content: [{ id: 1, text: 'hello' }].map(function(item) {
                var attrs = { value: item.id };

                return {
                    elem: 'option',
                    attrs: attrs,
                    content: item.text
                };
            }, this)
        }
    ]
}
```

Выше приведен синтетический пример, для которого есть более удобное решение в select__simple-filter
