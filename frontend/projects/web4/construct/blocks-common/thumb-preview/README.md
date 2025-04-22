# thumb-preview

Блок-микс для смены фреймов-превьюшек на заданной DOM node

Меняет либо `src` и `srcset` у элемента с тегом `img` либо, `background-image` у любого другого элемента

## Пример использования:
BEMJSON:
```js
{
    block: 'test',
    mix: {
        block: 'thumb-preview',
        js: {
            startDelay: 500,
            delay: 300,
            step: 1,
            infinite: true,
            thumbs: [
                ['http://nosite.nodomain/thumb-1.png'],
                ['http://nosite.nodomain/thumb-1.png'],
                ['http://nosite.nodomain/thumb-1.png']
            ]
        }
    },
    content: {
        block: 'image',
        url: 'http://nosite.nodomain/thumb-0.png',
        mix: {
            block: 'thumb-preview',
            elem: 'target'
        }
    }
}
```

JS:
```js
BEM.DOM.decl('test', {
    _onClick: function() {
        this.findBlockOn('thumb-preview').start();
    }
});
```

## Параметры блока

| Параметр        | Тип           | Обязательный  | Описание                                                 |
| --------------- | ------------- |:-------------:| -------------------------------------------------------- |
| thumbs          | String[][]    | +             | массив с ссылками на изображения                         |
| step            | Number        | +             | шаг смены превьюшек                                      |
| delay           | Number        | +             | задержка смены превьюшки                                 |
| startDelay      | Number        |               | задержка перед запуском показа превьюшек                 |
| infinite        | Boolean       |               | начинать показ превьюшек заново после показа последней   |

## BEM-события блока

| Событие         | Когда отсылается                                                                |
| --------------- | ------------------------------------------------------------------------------- |
| start           | после начала показа первой превьюшки                                            |
| change          | после смены каждой превьюшки                                                    |
| stop            | после остановки показа превьюшек                                                |
| end             | после показа последней превьюшки, если нет установлен параметр `infinite`       |
