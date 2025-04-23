Justifier выравнивает картинки по обоим краям, подобно `text-align: justify` для текста.

###Основные особенности
* Алгоритм выставляет последней картинке в последнем ряду фиксированную ширину
* Модификация equal-width помещает в ряды картинки однаковой ширины

###Как использовать (в priv.js)
var justifier = blocks['justifier'],
```js
    params = {
        maxRowWidth: 250,   // максимальная ширина ряда
        minImageWidth: 75,  // ширина, меньше которой картинка ужиматься не будет
        marginBetween: 10   // отступ между соседними картинками
    },
    thumbs = [
        { width: 100 },
        { width: 90 },
        { width: 80 },
        { width: 70 },
        { width: 60 }
    ],
    resultRows = justifier.getAlignedRows(thumbs, params);

console.log(resultRows);

    [{
        fullWidth: 290,
        thumbs: [{
            width: 100,
            alignedWidth: 82
        }, {
            width: 90,
            alignedWidth: 73
        }, {
            width: 80,
            alignedWidth: 75,
            preAligned: true
        }]
    }, {
        fullWidth: 140,
        thumbs: [{
            width: 70
        }, {
            width: 60
        }]
    }]
```

###benchmark на openstack
```
base x 284,109 ops/sec ±0.60% (95 runs sampled)
```
