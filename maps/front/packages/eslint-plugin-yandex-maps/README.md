# eslint-plugin-yandex-maps

Custom ESLint rules and configs for usage in Yandex Maps.

## Installation

```sh
npm i eslint eslint-plugin-yandex-maps --save-dev
```

## Configs
### `recommended`

* Usage:
    ```javascript
    // eslintrc.json

    {
        "extends": [
            // ...
            "plugin:yandex-maps/recommended"
        ]
    }
    ```

### `react`
* Usage:
    ```javascript
    // eslintrc.json

    {
        "extends": [
            // ...
            "plugin:yandex-maps/react"
        ]
    }
    ```

### `mocha`
* Usage:
    ```javascript
    // eslintrc.json

    {
        "extends": [
            // ...
            "plugin:yandex-maps/mocha"
        ]
    }
    ```

## Custom Rules Usage

```javascript
// eslintrc.json

{
  "rules": {
        "yandex-maps/asterisk-import": [
            "error",            // severity
            "react", "redux"    // array of options (stripped of brackets)
        ]
}
```

## Custom Rules List
`asterisk-import`

Forbids non-asterisk import from modules specified in options.

``` js
// Correct
import * as React from 'react';

// Incorrect
import React from 'react';
import {Component} from 'react';
import React, {Component} from 'react';
```

`function-name-signature-condition`

Sets limitations on function signature based on its name.

Example options:
``` json
    [
        {
            "name": "_?(has|have|had|is|are|was|were).*",
            "returnTypes": ["boolean", {"regex": ".* is .*"}]
        },
        {
            "name": "_?render.*",
            "requirements": [{
                "type": "class",
                "extends": "Component$"
            }],
            "returnTypes": ["React.ReactNode"]
        }
    ],
    {
        "promiseAllowed": true
    }
```
Based on these options:
- all functions matching regex `/_?(has|have|had|is|are|was|were).*/` will be treated as errors if they return a value of any other type than `boolean`, the one matching `/.* is .*/`, or a `Promise` of these types;
- all functions matching `/_?render.*/` in classes that extend identifiers ending with `Component` will be treated as errors if they return a value of any other type than `React.ReactNode` or `Promise<React.ReactNode>`;

`no-code-after-export`

Forbids any non-export code after the first export expression.

``` js
// Correct
fn();
export default a;

// Incorrect
export {a, b};
fn();
```
Rule options:

This rule is not configurable.

`no-code-before-import`

Forbids any non-import code before the last import expression.

``` js
// Correct
import default a;
var x = require('x');
fn();

// Incorrect
fn();
import default a;
var x = require('x');
```
Rule options:

This rule accepts an object with the only property:
``` javascript
{
    "ignoreDynamicImports": true
}
```
When set to `true`, dynamic import statements will not cause errors if there's code above them. Defaults to `false`.


## Contributing

See ESLint documentation for instructions on [how to write rules](https://eslint.org/docs/developer-guide/working-with-rules#rule-basics) and [how to write tests](https://eslint.org/docs/developer-guide/nodejs-api#ruletester).
Typings for rules and tests are available at [@typescript-eslint/experimental-utils](https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/experimental-utils) which is installed as a devDependency.

Put new rules in `src/rules`. 

Put tests in `src/tests`.

To test rules during development, run:
```
npm test
``` 

To lint files in `src/`, run: 
```
npm run lint
```

To test rules in an arbitrary project:
1. Run `npm run build`.
2. Copy `lib` folder and `package.json` to `node_modules/eslint-plugin-yandex-maps/` of your project.
3. Add rules to eslintrc.json as described in Custom Rules Usage section.
4. Lint your project as you normally do.

Update version and changelog, publish the new version on `npm.yandex-team.ru`.
