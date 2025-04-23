### Обертка всех cms виджетов

```js noeditor

```


```jsx
const logger = require('@yandex-market/logger');
const Provider = require('react-redux').Provider;
const createStore = require('redux').createStore;

logger.setup((_, err) => {
    // eslint-disable-next-line
    console.log(err);
}, 'error');

const Test = () => (<div style={{backgroundColor: 'red'}}>test widget</div>);

const store = createStore(() => ({
    collections: {},
}));

const props = {
  "nodes": [
      {
          "entity": "box",
          "name": "Grid12",
          "props": {
              "type": "row",
              "width": "default",
              "layout": true,
              "grid": 1
          },
          "nodes": [
              {
                  "entity": "box",
                  "name": "Grid12",
                  "props": {
                      "type": "column",
                      "layout": false,
                      "width": 1,
                      "position": "default"
                  },
                  "nodes": [
                      {
                          "entity": "widget",
                          "name": "Test",
                          "id": "936911-Header"
                      }
                  ]
              }
          ]
      }
  ],
  "mapping": {
    "Test": Test,
  },
};

<Provider store={store}>
    <Box {...props}/>
</Provider>
```
