
## Описание
Блок `clearfix` реализует популярный CSS-прием `clearfix`, также известный как [Easy Clearing Hack](http://www.456bereastreet.com/archive/200603/new_clearing_method_needed_for_ie7/).
Прием отменяет действие обтекания после плавающих HTML-элементов (с CSS-свойством `float`) расположенных внутри него и предотвращает сжимание по высоте родительского контейнера .

Блок реализован в технологии CSS. Файл содержит набор стилевых свойств, для одного из способов отмены действия обтекания и начала нового потока (использование псевдокласса `:after`).

При блочной верстке макета сайта применяются плавающие HTML-элементы, которые выпадают из основного потока (порядок вывода объектов на странице) и выходят за границы родительского элемента. В результате этого родительский элемент сжимается.

По умолчанию слои в потоке выстраиваются один под другим.
Плавающие элементы могут применяться для вывода слоев по горизонтали, например, добавление колонок.

### Объявление блока
Блок `clearfix` применяется либо самостоятельно, как контейнер c дочерними плавающими элементами, либо подмешивается к другому блоку-контейнеру содержащему плавающие элементы, BEMJSON:

```js
({
    block: 'x-area', // блок-контейнер с плавающими элементами
    mods: {bordered: 'yes', bg: 'squares'},
    attrs: {style: 'display: block'},
    mix: {block: 'clearfix'}, // блок для отмены обтекания дочерних элементов
    content: [
        {
            attrs: {style: 'float: left; height: 100px; width: 200px; background: #eda;'},
            content: 'text1, 200x100 px'
        },
        {
            attrs: {style: 'float: left; height: 100px; width: 200px; background: #ada;'},
            content: 'text2, 200x100 px'
        }
    ]
})
```


