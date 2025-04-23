## Описание

**Статус блока**: **deprecated**

Используется только в блоке `head-menu` и будет удален вместе с ним.

Блок `link-update-controller` – медиатор, обеспечивающий взаимосвязь между блоком `input`, расположенном в блоке [page-layout](../page-layout/page-layout.ru.md) и блоком [head-menu](../head-menu/head-menu.ru.md).
Он обновляет ссылки меню в `head-menu` согласно текущему значению `val` блока `input`, когда блок
 `page-layout` показывает панель `services`.


### Объявление блока на странице

BEMJSON для подключения блока:

```js
{
    block: 'page-layout',
    mix: [{ block: 'link-update-controller', js: true }],
    content: [
        {
            block: 'input',
            mix: [{ block: 'link-update-controller', elem: 'source' }] // микс элемента `source` к источнику данных
        },
        {
            block: 'head-menu',
            mix: [{ block: 'link-update-controller', elem: 'target'}], // микс элемента `target` к обновляемому блоку
            content: [
                {
                    block: 'link',
                    mix: [{ block: 'head-menu', elem: 'item'}],
                    url: '//m.images.yandex.ru/search'
                }
            ]
        }
    ]
}
```

### Принцип работы блока

Блок `link-update-controller` примешивается к блоку `page-layout`. Этот блок при открытии панелей генерирует событие `open`. `link-update-controller` подписывается на это событие и когда открывается панель `panel_type_services` вызывает свой метод `update()`.
Метод `update()` находит текущее значение блока `input` и передает его методу `updateLinks` блока `head-menu`.
