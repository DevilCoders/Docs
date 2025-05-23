# pt-flex

Блок для представления однострочных и многострочных секции с «плавающим» размером колонок.

### Модификаторы блока

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `view` | `stripe` | Тип отображения |
| `border` | `all` | Добавление рамок |
| `shadow` | `cloud` | Добавление тени |
| `status` | `default` `success` `warning` `alert` | Статус |
| `space-v` | `xs` `s` `m` `l` | Размер вертикального паддинга  |
| `space-h` | `xs` `s` `m` `l` | Размер горизонтального паддинга |
| `space-a` | `xs` `s` `m` `l` | Размер всех паддингов |

### Элементы блока

| Элемент | Описание |
| --------| -------- |
| [col](#elems-col) | Колонка |

```js

{
    block: 'pt-flex',
    mods: { view:'stripe', shadow: 'cloud', status: 'success', 'space-v': 'm', 'space-h': 'l' },
    content: [
        {
            elem: 'column',
            elemMods: { width: '40' },
            content: [
                Колонка
            ]
        },
        {
            elem: 'column',
            elemMods: { width: '30' },
            content: [
                Колонка
            ]
        },
        {
            elem: 'column',
            elemMods: { width: '30' },
            content: [
                Колонка
            ]
        }
    ]
}
```

### Элементы блока
 
<a name="elems-col"></a>
#### Элемент `col`

Колонка.

##### Модификаторы элемента блока

| Модификатор элемента | Допустимые значения | Описание |
| -------------------- | ------------------- | -------- |
| `align` | `center` `right` | Выравнивание |
| `width` | `5` `10` ... `100` | Ширина в процентах |
