# flow/force-type-arguments

Правило обязывает разработчика указывать аргументы в дженериках.

> Зачем?

Упрощаем себе переход на TypeScript, упрощаем обновление flow, улучшаем покрытие и DX.

## Примеры

Примеры **неправильного** кода

```js
// @flow

import {createAction} from 'redux-actions';
import {connect} from 'react-redux';

const doSomething = createAction(DO_SOMETHING);
const enhance = connect(mapStateToProps, mapDispatchToProps);

```

Примеры **правильного** кода

```js
// @flow

import {createAction} from 'redux-actions';
import {connect} from 'react-redux';

const doSomething = createAction<typeof DO_SOMETHING, Payload>(DO_SOMETHING);
const enhance = connect<State, Dispatch, OwnProps>(mapStateToProps, mapDispatchToProps);

```
