This webpack plugin transforms i18n calls into inline expressions.
## Usage
- Since this is an internal module you have to install it through the internal Github.
- Declare the plugin in `plugin` section.
```js
var i18n = require('@ps-int/webpack-i18n-plugin');
var dictionary = require('someLanguage.js');
var fallbackDictionary = require('defaultLanguage.js');

module.exports = {
    plugins: [
        new i18n(dictionary, fallbackDictionary, 'i18n')
    ]
}
```
