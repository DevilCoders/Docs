## mi-sticky-list

Блок, позволяющий заголовки в списке при прокрутке страницы сделать прилипающими и плавно сменяющими друг друга.

### Использование

* Блоку, в котором будет содержаться список, примешиваем блок `mi-sticky-list`. Этому блоку будет добавлено CSS-свойство `overflow: hidden;`. Блок должен иметь значение свойства `position` отличное от `static`.
* Внутри блока создаем блок списка и примешиваем ему элемент `blocks-wrapper` блока `mi-sticky-list`. Этому блоку будет добавлено CSS-свойство `overflow: auto;`. CSS-свойство `position` этого блока должно быть `static`.
* К каждому элементу списка примешиваем блок `mi-sticky-list-block`.
* Заголовку в элементе списка примешиваем элемент `item` блока `mi-sticky-list-block`.

### Пример использования

```js
{
    block: 'b-tabbed-panel',
    mods: {'panel-state': 'current'},
    mix: [{ block: 'mi-sticky-list', js: 'true'}],
    content: [
        {
            block: 'b-sidebar-list',
            mix: [{ block: 'mi-sticky-list', elem: 'blocks-wrapper' }],
            content: [
                {
                    block: 'b-sidebar-block',
                    mix: [{block: 'mi-sticky-list-block'}],
                    content: [
                        {
                            elem: 'head',
                            mix: [{block: 'mi-sticky-list-block', elem: 'item'}],
                            content: '1 Заголовок блока с текстом-рыбой'
                        },
                        {
                            elem: 'content',
                            content: 'Текст рыба который показывает нормальное распределение букв в строках и в массиве текста по блоку. Всё это нужно для моделирования поведения блока и элемента в реальной ситуации.'
                        }
                    ]
                },
                {
                    block: 'b-sidebar-block',
                    mix: [{block: 'mi-sticky-list-block'}],
                    content: [
                        {
                            elem: 'head',
                            mix: [{block: 'mi-sticky-list-block', elem: 'item'}],
                            content: '2 Заголовок блока с текстом-рыбой'
                        },
                        {
                            elem: 'content',
                            content: 'Текст рыба который показывает нормальное распределение букв в строках и в массиве текста по блоку. Всё это нужно для моделирования поведения блока и элемента в реальной ситуации.'
                        }
                    ]
                },
                {
                    block: 'b-sidebar-block',
                    mix: [{block: 'mi-sticky-list-block'}],
                    content: [
                        {
                            elem: 'head',
                            mix: [{block: 'mi-sticky-list-block', elem: 'item'}],
                            content: 'N Заголовок блока с текстом-рыбой'
                        },
                        {
                            elem: 'content',
                            content: 'Текст рыба который показывает нормальное распределение букв в строках и в массиве текста по блоку. Всё это нужно для моделирования поведения блока и элемента в реальной ситуации.'
                        }
                    ]
                }
            ]
        }
    ]
}
```
