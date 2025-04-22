# Особенный импорт React-компонентов

Возможность подключать декларации блоков, элементов и модификаторов с разных уровней переопределения реализуется с помощью особенного синтаксиса импортов нового стандарта ES2015. Путь до импортируемой сущности представляет из себя строковую запись из имени и модификаторов, которые после обработки траншпиллером раскрываются в правильную последовательность из стандартных `require`.

## Концепция

Допустим, у нас есть декларация блока:
``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'hello',
    // ...
});
```

Чтобы использовать этот блок в другом модуле, необходимо написать импорт следующего вида:
``` js
import Hello from 'b:hello';

ReactDOM.render(
    <Hello />,
    //...
);
```

Данная запись будет трансформирована в следующее:
``` js
var Hello = [
    require('path/to/hello/hello.js')
][0].applyDecls();

ReactDOM.render(
    <Hello />,
    //...
);
```

Допустим, что наш блок представлен на 3х уровнях: `common`, `deskpad`, `desktop`. Тогда наша запись будет трансформирована следующим образом:

``` js
import Hello from 'b:hello';
```

``` js
var Hello = [
    require('path/to/common/hello/hello.js'),
    require('path/to/deskpad/hello/hello.js'),
    require('path/to/desktop/hello/hello.js')
][0].applyDecls();
```

__NB:__ Никакой магии не происходит, и синтаксис импортов — не более чем синтаксический сахар над последовательностью из `require`. Кроме того, такой подход позволяет не запоминать весь список уровней и их порядок для подключения сущности — траншпиллер делает эту работу автоматически.

_На самом деле результирующее выражение немного сложнее, в нем проверяются способы импортов и экспортов модулей, но в общем случае выражение выглядит именно так._

#### Подключение других технологий

Предположим, у нашего блока кроме JS-реализации есть еще и CSS. Система импортов, вкупе со сборщиками вроде Webpack, позволяет подключать в том числе и CSS — это произойдет автоматически. Список подключаемых технологий задается в конфиге траншпиллера. В данном случае наша запись будет трансформирована следующим образом:

``` js
import Hello from 'b:hello';
```

``` js
var Hello = [
    require('path/to/common/hello/hello.js'),
    require('path/to/deskpad/hello/hello.js'),
    require('path/to/desktop/hello/hello.js'),
    require('path/to/common/hello/hello.css'),
    require('path/to/desktop/hello/hello.css')
][0].applyDecls();
```

__NB:__ Кроме создания последовательности из `require`, траншпиллер выполняет дополнительную работу по поиску файлов технологии на файловой системе. Это позволяет подключать только те `require`, которые действительно существуют на файловой системе.

#### Только CSS

Бывает, что БЭМ-сущности выражены только в технологии CSS. Траншпиллер достаточно умен, чтобы обработать такую ситуацию. В данном случае наша запись будет трансформирована в следующее:


``` js
import Hello from 'b:hello';
```

``` js
var Hello = [
    require('path/to/common/hello/hello.css'),
    require('path/to/desktop/hello/hello.css')
];
```

#### Импорт без переменной

Это стандартная возможность системы импортов. Реализация особенного синтаксиса никак не влияет на это. Подобный импорт мог бы выглядеть так:

``` js
import 'b:hello';
```

Результат:

``` js
([
    require('path/to/common/hello/hello.css'),
    require('path/to/desktop/hello/hello.css')
]);
```

## Синтаксис

### Блок

``` js
import Block from 'b:block';
```

#### Блок с булевым модификатором

``` js
import Block from 'b:block m:modName';
```

#### Блок с модификатором в значении

``` js
import Block from 'b:block m:modName=modVal';
```

#### Блок с модификатором и его несколькими значениями

``` js
import Block from 'b:block m:modName=modVal1|modVal2';
```

#### Блок с несколькими модификаторами

``` js
import Block from 'b:block m:modName1 m:modName2=modVal1|modVal2';
```

### Элемент

``` js
import BlockElem from 'b:block e:elem';
```

#### Элемент с булевым модификатором

``` js
import BlockElem from 'b:block e:elem m:modName';
```

#### Элемент с модификатором в значении

``` js
import BlockElem from 'b:block e:elem m:modName=modVal';
```

#### Элемент с модификатором и его несколькими значениями

``` js
import BlockElem from 'b:block e:elem m:modName=modVal1|modVal2';
```

#### Элемент с несколькими модификаторами

``` js
import BlockElem from 'b:block e:elem m:modName1 m:modName2=modVal1|modVal2';
```

## Контекст

Синтаксис импортов понимает текущий контекст, что позволяет в декларации блока импортировать свои элементы без дублирования имени блока:

``` js
import {decl} from 'bem-react-core';
// point your eyes here
import Elem from 'e:elem';

export default decl({
    block: 'hello',
    content() {
        return [
            <Elem key='elem' />,
            'World'
        ];
    }
});
```

## Траншпиллеры

На данный момент существует два способа работы с системой импортов: [лоадер для Webpack](https://github.com/bem/webpack-bem-loader) и [плагин для Babel](https://github.com/bem/babel-plugin-bem-import). Разница между ними описана в [FAQ](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/projects/lego/guidelines/react-faq.md) по работе с React. Настройка плагина выполняется в 2 простых и привычных для всех шага.

#### Webpack

> npm i -D bem/webpack-bem-loader

После установки необходимо дополнить `webpack.config.js` настройками для лоадера:

``` js
module.exports = {
    //...
    module: {
        loaders: [{
            test: /\.js$/,
            exclude: /node_modules/,
            loaders: ['webpack-bem', 'babel']
        },
        //...
    },
    bemLoader: {
        naming: {
            // Опционально, переопределения для неймига
        },
        techs: ['js', 'css'],
        levels: [
            'path/to/common',
            'path/to/desktop'
        ]
    },
    //...
}
```

__NB:__ Важно, чтобы до любой другой обработки JS-файлов лоадер уже был.

#### Babel

> npm i -D bem/babel-plugin-bem-import

После установки необходимо дополнить  `.babelrc` настройками для плагина:

``` js
{
    "plugins": [
        ["bem-import", {
            "naming": {
                // Опционально, переопределения для неймига
            },
            "levels": [
                'path/to/common',
                'path/to/desktop'
            ],
            "techs": ["js", "css"]
        }]
    ]
}
```
