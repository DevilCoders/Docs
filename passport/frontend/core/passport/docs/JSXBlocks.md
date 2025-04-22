# React компоненты

Новые блоки (компоненты) создаем в папке `blocks/react-blocks`. В качестве [библиотеки контролов][5] используем `lego-on-react`.

## React
* Создаем папку для компонента. Например, `blocks/react-blocks/Block`;
* Создаем view - `blocks/react-blocks/Block/Block.jsx`;
* Создаем файл стилей - `blocks/react-blocks/Block/Block.styl`; (если актуально)
* Создаем index.js - `blocks/react-blocks/Block/index.js`. В нем либо просто экспорт класса, либо его коннект к стору, mapStateToProps/mapDispatchToProps и экспорт. Не экспортируем default, ибо явное лучше неявного;
* Profit...;
* Вы прекрасны;

#### Пример простого компонента

```jsx
// blocks/react-blocks/Block/Block.jsx

import './Block.styl'
import React from 'react';
import Link from 'lego-on-react/src/components/link/link.react';
import {cn} from '@bem-react/classname';

const b = cn('Block');

class Block extends React.PureComponent {
    render() {
        return(
            <div className={b()}>
                <Link
                    theme='normal'
                    url='/url'
                    text={ i18n('tanker.key') } />
            </div>
        )
    }
}

export {Block};
```

```jsx
// blocks/react-blocks/Block/Block.styl

.Block
  background: red
```

```js
// blocks/react-blocks/Block/index.js

import {connect} from 'react-redux';
import {updateValues} from '@blocks/actions/form';
import {hasExp, isGDPR} from '@blocks/selectors';
import {Block} from './Block.jsx';

const mapStateToProps = (state = {}) => ({
    isGDPR: isGDPR(state),
    isExp: hasExp(state, 'exp-name')
});

const mapDispatchToProps = {
    updateValues
};

const ConnectedBlock = connect(mapStateToProps, mapDispatchToProps)(Block);

export {ConnectedBlock as Block};
```

```jsx
// blocks/react-blocks/AnotherBlock/AnotherBlock.jsx

import React from 'react';
import {Block} from '@blocks/Block';

class AnotherBlock extends React.PureComponent {
    render() {
        return(
            <Block />
        )
    }
}

export {AnotherBlock};
```

## Redux
Документация [en][2] | [rus][3]. Redux требует наличие [actions][6] и [reducers][7], именуем соответсвенно и кладем в папку с компонентом ([например][8]) и не забываем подключать в рутовый редьюсер.

## Реиспользуемые компоненты и экраны

Если смысловая нагрузка вашего компонента намекает на то, что он может быть переиспользован, то скорее всего так и будет. Многие процессы сейчас перетекают в домик, и во многих из них есть одинаоквые этапы: подтвердить телефон, показать найденные аккануты, показать глобальную ошибку, etc. Такие компоненты стоит складывать в папку Screens. В ней раскладываем компоненты согласно здравому смыслу: специфичные для регистрации - кладем в SignUp, может использоваться для любого процесса - кладем в корень.

Такая же история с условными лего-компонентами: Title, Header, Footer, Button, Field, etc ... Более низкоуровневые элементы, которые могут вам потребоваться на любой странице. Все это складываем в Components.

[2]: http://redux.js.org/docs/basics/ExampleTodoList.html
[3]: https://rajdee.gitbooks.io/redux-in-russian/content/index.html
[4]: https://jing.yandex-team.ru/files/y-i-demin/2016-06-07_18-05-46.png
[5]: https://lego.yandex-team.ru/lego-on-react/
[6]: http://redux.js.org/docs/basics/Actions.html
[7]: http://redux.js.org/docs/basics/Reducers.html
[8]: https://github.yandex-team.ru/passport-frontend/core/tree/develop/passport/blocks/react-blocks/avatar-displayname
