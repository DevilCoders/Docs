# @vertis/connect-contimer

## Usage

```js
var connect = require('connect'),
    timer = require('@vertis/connect-contimer'),
    app = connect();

app.use(timer(function(time, req) {
    console.log('Response processing time %s ms', time);
}));
```
