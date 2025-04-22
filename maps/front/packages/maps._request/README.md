# `@yandex-int/maps._request`

## Usage

With default logger:

```js
const request = require('@yandex-int/maps._request');

const {body} = await request('/path', {query: {a: 1}});
```

With own instance of `winston.Logger`:

```js
const {createLogger} = require('@yandex-int/maps-logger');
const createRequest = require('@yandex-int/maps._request');

const logger = createLogger({
    tskvFormat: 'label'
});
const request = createRequest(logger);

const {body} = await request('/path', {query: {a: 1}});
```
