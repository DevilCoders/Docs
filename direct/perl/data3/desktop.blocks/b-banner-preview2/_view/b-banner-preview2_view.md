####Как создать новый view (вид превью, например: базовый вид, на десктопном поиске, на мобильном поиске, ...)
1. Создаем `bemhtml`-файл нового view и описываем моду `content`. Можно менять разметку как необходимо, в контексте элементов данные не передаем, папки для элементов присущих только этому view не создаем.
2. Элементы универсальные для всех view, есть возможность переопределить для конкретного. Если нужного элемента не хватает - создаем новый. В `bemhtml` данные будут доступны в глобальном `this.ctxData`
3. В `u-utils__b-banner-preview2.js` есть метод `fromServer`, он преобразовывает данные для `b-banner-preview2` из серверных данных баннера. Дополняем его новыми полями, если нужно

```js
({
    block: 'b-banner-preview2',
    mods: { view: 'new-view' },
    data: u['b-banner-preview2'].fromServer()
})
```

####Как сделать view самообновляющийся при изменении модели
1. Добавляем модификатор `_repaint_yes`
2. В `b-banner-preview2_repaint_yes.js` доопределяем метод `_dependsCtxDataFromModelFields` новыми зависимостями входных данных блока от полей модели баннера
3. В `u-utils__b-banner-preview2.js` в методе `fromModel` описываем как получить новые входные данные из модели
4. Создаем `js`-файл для view, в котором описан метод `_getElemsDepends` с зависимостями элементов от изменения входных данных, т.е. ключом объекта является поле входных данных, при изменении которого нужно перерисовать элементы указанные в значении.

```js
({
    block: 'b-banner-preview2',
    mods: { view: 'new-view' },
    data: u['b-banner-preview2'].fromServer()
})
```
