# pt-list

Паттерн для описание списка похожих друг на друга вертикально перечисленных сущностей.

### Модификаторы блока

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `view` | `default` `ghost` | Тип отображения |
| `border` | `all` | Добавление рамок |
| `shadow` | `cloud` | Добавление тени |

### Элементы блока

| Элемент | Описание |
| --------| -------- |
| [item](#elems-item) | Элемент |

```js
{
    block: 'pt-list',
    mods: { border: 'all', view: 'default' },
    content: [
        {
            elem: 'list',
            elemMods: { 'space-a': 'xl', border: 'bottom' },
            content: 'item'
        },
        {
            elem: 'list',
            elemMods: { 'space-a': 'xl', border: 'bottom' },
            content: 'item'
        },
        {
            elem: 'list',
            elemMods: { 'space-a': 'xl', border: 'bottom' },
            content: 'item'
        }
    ]
}
```

### Элементы блока

<a name="elems-item"></a>
#### Элемент `item`

Элементы item могут включать в себя друг друга.

##### Модификаторы элемента блока
 
| Модификатор элемента | Допустимые значения | Описание |
| -------------------- | ------------------- | -------- |
| `border` | `bottom` `top` | Рамки |
| `indent-t` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешний отступ сверху |
| `indent-r` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешний отступ справа |
| `indent-l` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешний отступ слева |
| `indent-b` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешний отступ внизу |
| `indent-v` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешние отступы по вертикали |
| `indent-h` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешние отступы по горизонтали |
| `indent-a` | `xs` `s` `m` `l` `xl` `xxl` `xxxl` | Внешние отступы по всем сторонам |
| `space-t` | `xxs` `xs` `s` `m` `l` `xl` `xxl` | Внутренний отступ сверху |
| `space-r` | `xxs` `xs` `s` `m` `l` `xl` `xxl` | Внутренний отступ справа |
| `space-l` | `xxs` `xs` `s` `m` `l` `xl` `xxl` | Внутренний отступ слева |
| `space-b` | `xxs` `xs` `s` `m` `l` `xl` `xxl` | Внутренний отступ внизу |
| `space-v` | `xxs` `xs` `s` `m` `l` `xl` `xxl` | Внутренние отступы по вертикали |
| `space-h` | `xxs` `xs` `s` `m` `l` `xl` `xxl` | Внутренние отступы по горизонтали |
| `space-a` | `xxs` `xs` `s` `m` `l` `xl` `xxl` | Внутренние отступы по всем сторонам |
| `distribute` | `between` `default` | Распределение контента внутри item по горизонтали|
| `vertical-align` | `center` `top` | Выравнивание контента внутри item по вертикали|
