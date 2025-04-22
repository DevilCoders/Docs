# node-tanker
Node-tanker downloads and converts localization into javascript modules for each language

## Usage
- Since this is an internal module you have to install it through the internal Github.
- Include module as it shown below.
```js
var Tanker = require('node-tanker');

var tanker = new Tanker({
    "project": "mail",
    "languages": [ "ru", "en" ],
    "modules": [
        "common",
        "mobile",
        "promo"
    ],
    "path": "./dir",
    // it's necessery for runtime transformations
    "namespace": "qu"
});
```
- Just use it!
```js
tanker.dump().then(tanker.toJS, tanker);
```

That's all. Simple and fast.
