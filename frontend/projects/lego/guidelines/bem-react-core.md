# BEM React Core

Библиотека для описания React-компонентов в виде деклараций БЭМ-сущностей. Библиотека работает поверх обычных React-компонентов и предоставляет набор функций для описания деклараций блоков, элементов и модификаторов, а также набор дополнительных методов для React-компонентов, синтаксис которых схож с модами `BEMHTML`. Наравне с этим также работают нативные методы React-компонентов. Разработка библиотеки ведётся в [Open Source](https://github.com/bem/bem-react-core). Описание деклараций работает в совокупности с [особенным синтаксисом импортов](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/projects/lego/guidelines/bem-react-import.md) нового стандарта.

Простой пример:
``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'hello',
    content() {
        return 'world';
    }
});
```

Результат:
``` html
<div class='hello'>world</div>
```

Тот же код без декларации:
``` js
import React, {Component} from 'react';

export default class Hello extends Component {
    render() {
        return (
            <div className='hello'>world</div>
        );
    }
}
```

## Декларации

#### Блок

``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    content() {
        return 'content goes here';
    }
});
```
Результат:
``` html
<div class='my-block'>content goes here</div>
```

#### Элемент

``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    elem: 'my-elem',
    content() {
        return 'elem content goes here';
    }
});
```
Результат:
``` html
<div class='my-block__my-elem'>elem content goes here</div>
```

#### Модификатор

Декларация модификатора принимает первым аргументом функцию-матчер, которая возвращает значение булева типа. Функция-матчер в качестве аргумента принимает объект пропсов и может содержать любые условия. Если функция-матчер возвращает положительное значение, декларация применяется к сущности.

``` js
import {declMod} from 'bem-react-core';

export default declMod(({theme}) => theme === 'normal', {
    block: 'my-block',
    mods({theme}) {
        return {theme};
    },
    content() {
        return 'content with theme normal goes here';
    }
});

// <MyBlock theme='normal' />
```
Результат:
``` html
<div class='my-block my-block_theme_normal'>content with theme normal goes here</div>
```

#### Булевые модификаторы

``` js
import {declMod} from 'bem-react-core';

export default declMod(({simple}) => simple, {
    block: 'my-block',
    mods({simple}) {
        return {simple};
    },
    content() {
        return 'content with simple goes here';
    }
});

// <MyBlock simple />
```
Результат:
``` html
<div class='my-block my-block_simple'>content with simple goes here</div>
```

#### Несколько модификаторов

``` js
export default declMod(({theme}) => theme === 'normal', {
    // ...
    mods({theme}) {
        return {...this.__base.apply(this, arguments), theme};
    },
    // ...
});

export default declMod(({simple}) => simple, {
    // ...
    mods({simple}) {
        return {...this.__base.apply(this, arguments), simple};
    },
    // ...
});

// <MyBlock theme='normal' simple />
```
Результат:
``` html
<div class='my-block my-block_theme_normal my-block_simple'>content with simple goes here</div>
```

## Стандартные методы и поля деклараций

Все методы деклараций принимают в качестве аргумента объект пропсов. Исключение составляют метод `wrap`, который принимает в качестве аргумента сам компонент, и метод `content`, который кроме пропсов в качестве первого аргумента принимает поле пропсов `children` в качестве второго. Второй аргумент был добавлен для удобства, так как это поле используется чаще остальных.

#### block

Имя блока. Будет транслировано в соответствующий класс узла.

``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    // ...
});
// <MyBlock />
```
Результат:
``` html
<div class='my-block'></div>
```

#### elem

Имя элемента блока. Транслируется в соответствующий класс узла.

``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    elem: 'my-elem',
    // ...
});
// <MyBlockElem />
```
Результат:
``` html
<div class='my-block__my-elem'></div>
```

#### tag

HTML-тэг узла. По умолчанию `div`.

``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    tag: 'span',
    // ...
});

// <MyBlock />
```
Результат:
``` html
<span class='my-block'></span>
```

#### attrs

HTML-атрибуты узла.

``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    attrs({id}) {
        return {id, tabIndex: -1}
    },
    // ...
});

// <MyBlock id='the-id' />
```
Результат:
``` html
<div class='my-block' id='the-id' tabindex='-1'></div>
```

#### mods

Модификаторы сущности. Весь список будет транслирован в соответствующие классы узла.

``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    mods({disabled}) {
        return {disabled, forever: 'together'}
    },
    // ...
});

// <MyBlock disabled />
```
Результат:
``` html
<div class='my-block my-block_forever_together my-block_disabled'></div>
```

#### content

Контент узла.

``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    content({greeting}, children) {
        return `${greeting}, ${children}`;
    },
    // ...
});

// <MyBlock greeting='Mr'>grape</MyBlock>
```
Результат:
``` html
<div class='my-block'>Mr, grape</div>
```

#### wrap

Специальный метод, позволяющий обернуть компонент в дополнительный узел.

``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    wrap(component) {
        return (
            <section>{component}</section>
        );
    },
    // ...
});

// <MyBlock />
```
Результат:
``` html
<section><div class='my-block'></div></section>
```

## Стандартные методы React

#### Lifecycle hooks

Доопределение методов React заключалось в переименовании ‒ имена теперь не содержат слова `component`. Это позволяет работать в терминах БЭМ, кроме того, эти методы могут быть доопределены на других уровнях. Официальная документация [тут](https://facebook.github.io/react/docs/react-component.html).

``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    willMount() {
        // оригинальное имя: componentWillMount
    },
    didMount() {
        // оригинальное имя: componentDidMount
    },
    willReceiveProps() {
        // оригинальное имя: componentWillReceiveProps
    },
    shouldUpdate() {
        // оригинальное имя: shouldComponentUpdate
    },
    willUpdate() {
        // оригинальное имя: componentWillUpdate
    },
    didUpdate() {
        // оригинальное имя: componentDidUpdate
    },
    willUnmount() {
        // оригинальное имя: componentWillUnmount
    }
    // ...
});
```

#### Конструктор

Базовый конструктор также был доопределен, чтобы обеспечить гибкое доопределение на других уровнях.

``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    willInit() {
        // оригинальное имя: constructor
    },
    // ...
});
```

Остальные методы остались без изменений.

__NB:__ метод `render` перезаписывает весь узел целиком, при его использовании игнорируется генерация классов, стандартные поля и методы декларации (иногда это действительно необходимо).

## Механизм доопределений

Любое поле или метод декларации могут быть доопределены на других уровнях. Это возможно благодаря особенному наследованию, которое реализуется с помощью модуля [inherit](https://github.com/dfilatov/inherit). Доопределяться могут как стандартные методы и поля декларации, так и доопределенные методы React.

Например, описываем блок на уровне 1:
``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    attrs({id}) {
        return {id};
    },
    content({greeting}, children) {
        return `${greeting}, ${children}.`;
    }
});
```
И доопределяем его на уровне 2:
``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    attrs() {
        return {...this.__base.apply(this, arguments), tabIndex: -1};
    },
    content({message}) {
        return `${this.__base.apply(this, arguments)} ${message}.`;
    }
});

// <MyBlock id='the-id' greeting='Mr' message='I love you!'>grape</MyBlock>
```

Результат:
``` html
<div class='my-block' id='the-id' tabindex='-1'>Mr, grape. I love you!</div>
```

## Биндинги

Стандартные биндинги передаются через метод `attrs` наравне с атрибутами узла. Как и в оригинальном классе, они декларируются в виде метода класса.

``` js
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    willInit() {
        this.onClick = this.onClick.bind(this);
    },
    attrs() {
        return {onClick: this.onClick};
    },
    onClick(e) {
        console.log('Wow! You can click!');
    }
});
```

## Статические методы

Декларируются вторым аргументом функции декларации `decl` или `declMod`.

``` js
import {PropTypes} from 'prop-types';
import {decl} from 'bem-react-core';

export default decl({
    block: 'my-block',
    content() {
        return this.__self.customMethod();
    }
}, {
    propsTypes: {
        theme: PropTypes.string.isRequired,
        size: PropTypes.oneOf(['s', 'm', 'l'])
    },
    defaultProps: {
        theme: 'normal'
    },
    customMethod() {
        console.log('static method call');
        return 'default content';
    }
});
```

## Наследование

В отличие от `i-bem` реализации, элементы в `bem-react-core` обладают абсолютно теми же свойствами и возможностями, что и блоки. Благодаря этому мы можем наследовать не только блоки от других блоков, но и элементы от блоков и блоки от элементов.

``` js
export default decl(Entity, {
    block: 'my-block'
});

export default decl(Entity, {
    block: 'my-block',
    elem: 'my-elem'
});
```

Также допустимо наследование от нескольких сущностей.

``` js
export default decl([Entity1, Entity2, ...], {
    block: 'my-block'
});

export default decl([Entity1, Entity2, ...], {
    block: 'my-block',
    elem: 'my-elem'
});
```
