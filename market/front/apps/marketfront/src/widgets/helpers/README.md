## API of helpers

### `connectWidget([mapStateToProps], [mapDispatchToProps], [mergeProps], [options])`

Связывает виджет со store и проверянет наличие в нем данных,
если данных нет, то не показывает виджет,таким образом
предотврощается отрисовка пустой секции с заголовком.

Имеет точно такую же сигнатуру как
[react-redux/connect](https://github.com/reactjs/react-redux/blob/master/docs/api.md#connectmapstatetoprops-mapdispatchtoprops-mergeprops-options),
но **предпологается что в store у виджета есть поле `data`**, а если нет или оно пустое, то он не будет отрисован.

```js
// state
{
  widgets: {
    WidgetArea: {
      6543210: {
        id: 6543210,
        // обязательное наличие поля data, иначе виджет не будет отрисован
        data: [
          // ...
        ],
        props: {
          // ...
        },
      },
    },
  },
}
```

```js
import connectWidget from '@self/root/src/legacy/connectWidget';

// ...

function mapStateToProps(state, props) {
  return {
    data: getWidgetData(state, props),
    ...getWidgetProps(state, props),
  };
}

function mapDispatchToProps(dispatch, {id}) {
  return {
    onClickMore: () => dispatch(doSomething({id}))
  };
}

export default connectWidget(
  mapStateToProps,
  mapDispatchToProps
)(Widget, 'WidgetArea');
```


### `createConnectWidget([path])`

Создает `connectWidget`, который проверяет заданное в `path` свойство.

* `[path: Array:<string> = ['data']]` Путь до свойства, которое проверять на пустоту (`isEmpty`).


```js
// state
{
  widgets: {
    WidgetArea: {
      6543210: {
        id: 6543210,
        data: {
          data: [
            // ...
          ],
          props: {
            // ...
          },
        },
      },
    },
  },
}
```

```js
import {createConnectWidget} from '@self/root/src/legacy/connectWidget';

// ...

export default createConnectWidget(
    ['data', 'data']
)(
  mapStateToProps,
  mapDispatchToProps
)(Widget, 'WidgetArea');
```


### `createLookup(lookup, [defaultProps])`

Создает функции iteratee, которая для каждой сущности вызывает нужный контейнер.
Используется когда виджет может отрисовывать несколько типов сущностей.

* `lookup: Object` Объект, где свойствами являются типы сущностей (schema), а значениями компоненты (Entity).

```js
// lookup.js
import {Formula} from 'entities/formula/Formula';

export default {
  formula: Formula,
};
```

* `[defaultProps]` Props которые будет передано во все компоненты.
```js
// state
{
  widgets: {
    Showcase: {
      6543210: {
        id: 6543210,
        // обязательное наличие поля data, иначе виджет не будет отрисован
        data: [
          {
            id: 1,
            schema: 'navnode',
          },
          {
            id: 2,
            schema: 'navnode',
          },
          {
            id: 3,
            schema: 'navnode',
          },
          {
            id: 1,
            schema: 'formula',
          },
          {
            id: 2,
            schema: 'formula',
          },
          {
            id: 3,
            schema: 'formula',
          },
          {
            id: 1,
            schema: 'picture',
            // ...
          },
          {
            id: 1,
            schema: 'thumbnail',
            // ...
          },
        ],
        props: {
          // ...
        },
      },
    },
  },
}
```
```js
// ...

const lookup = {
  formula: Formula,
  navnode: Navnode,
  // Значение по умолчанию, для всех schema, кроме formula и navnode
  default: Thumb,
}

function Widget({
  data,
  size,
  theme,
}) {
  // Будет передано всем компонентам Formula, Navnode и Thumb
  const defaultShowcaseItemProps = {size, theme};

  return (
    <Showcase>
      {data.map(createLookup(lookup, defaultShowcaseItemProps))}
    </Showcase>
  );
}
```
