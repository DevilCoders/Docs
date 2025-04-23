maps-tslint-ruleset
------------

Custom Yandex.Maps lint rules for [TSLint](https://github.com/palantir/tslint/).

### Installation and usage

```
npm i --save-dev tslint @yandex-int/maps-tslint-ruleset
```

To use these lint rules with the default configuration, use inheritance via the `extends` keyword.
Here's a sample configuration:

```js
{
  "extends": ["yandex-maps-tslint-ruleset"],
  "rules": {
    // override rules from the set
    "no-inline-export": false
  }
}
```

### Rules

- `asteriks-import`
  - Forbids non-asteriks import of modules specified in options.
  ```ts
  // Good:
  import * as React from 'react';

  // Bad:
  import React from 'react';
  ```
  - Rule option: `["react", "react-redux", ...]`.
  - This rule has a fixer.
- `class-members-order`
  - Enforces the order of class members.
  - Rule options:
  ```ts
  [{
      "regexp": "^_private",
      "position": 1
  }, {
      "regexp": "render.",
      "modifier": "private",
      "position": 3
  }, {
      "regexp": "render",
      "modifier": "protected",
      "position": 2
  }, {
      "regexp": "render",
      "position": 5
  }, {
      "position": 0
  }]
  ```
  Options must be sorted narrowing as the first matching option will be chosen.
  Every option has to be of type `SortOption`. The option without a regexp represents the rest of class members.
  ```ts
  type StringModifier = 'AsyncKeyword' | 'PublicKeyword' | 'PrivateKeyword' | 'ProtectedKeyword' | 'StaticKeyword';

  interface SortOption {
      regexp?: string;
      modifier?: StringModifier;
      position: number;
  }
  ```
  Sort option has to have a position in sorting order, may have a regexp template string to match with the class member name and a modifier.

- `default-import-naming`
  - Enforces default import variable name convention.
  - Example rule options (with explanations):
  ```ts
  [true, {
    // files that start with react-dom
    "filter": "^react-dom"
    "options": [
      [
        // have to be named exactly ReactDom
        {"exact": "ReactDom"}
      ]
    ]
  }, {
    // files that end up with dot and extension
    "filter": "\\..*",
    "options": [
      // have to comply with this (only) option:
      [
        // remove ".foo" part;
        {"from": "\\..*", "to": ""},
        // then camelCase name;
        "camelCase",
        // then add "Url" in the end.
        {"from": ".$", "to": "$&Url"}
      ]
      // module "foo-boingo.bar" have one valid name "fooBoingoUrl"
    ]
  }, {
    // the rest of the files (no filter option)
    "options": [
      // will have to either comply to PascalCase
      "PascalCase",
      // or camelCase
      "camelCase"
    ]
  }]
  ```
  - Supported transforms: `camelCase`, `PascalCase`, `snake_case`, transforms of type `{from: string, to: string}` and transform of type `{exact: string}`.
  
  The fixer is available if only one option is set in rule options.
- `function-name-signature-condition`
  - Sets limitations on function signature based on its name.
  - Example rule options:
    ```ts
    [
      true,
      [{
        name: "_?on.*",
        restrictions: [{
          type: 'class',
          extends: 'Component$'
        }]
        returnTypes: ["void"]
      }],
      {promiseAllowed: true}
    ]
    ```
  Based on those options all functions complied to regex `_?on.*` in classes which extend identifiers that end with `Component` will be treated as errors if return any type other than `void` or `Promise<void>`. 

- `jsx-node-condition`
  - Specifies condition-based rules on JSX nodes.
  - Example rule options:
    ```ts
    [{
      "filter": {
        "type": "tag"
      },
      "conditions": [
        {
          "ifThis": {
            "type": "child",
            "condition": {
              "type": "attribute",
              "attributeName": "fooConditionAttr",
              "validator": "exists"
            }
          },
          "thenThat": [
            {
              "type": "attribute",
              "attributeName": "fooResolutionAttr",
              "validator": "exists"
            }
          ]
        }
      ]
    }]
    ```
    Those options required any JSX tag that has a child with `fooConditionAttr` attribute to have `fooResolutionAttr` attribute.
    See source code for more detailed types.
- `multiline-parameters`
  - Enforces breaks between parentheses and parameters.
  - Rule options is an object with two arguments:
  ```ts
  interface Options {
    args?: 'same' | 'different' | 'consistent' | 'consistent-with-parens';
    parens?: 'same' | 'different' | 'consistent';
  }
  ```
  - `parens` `same` option forces parentheses to be always on the same line.
  - `parens` `different` option forces parentheses to be always on different lines.
  - `parens` `consistent` option forces both parentheses to be either adjacent to parameters or non-adjacent to parameters.
  - `args` `same` option forces arguments to be always on the same line.
  - `args` `different` option forces arguments to be always on different line.
  - `args` `consistent` option forces arguments to be either all on the same or all on different lines.
  - `args` `consistent-with-parens` option forces the same as `consistent` option; besides if the parentheses are not adjacent to parameters it forces them to be on different lines.
- `no-code-after-export`
  - Forbids any non-export code after first export expression.
  ```ts
  // Good:
  fn();
  export default a;

  // Bad:
  export {a, b};
  fn();
  ```
  - This rule has a fixer (though it is not aware of indentations in the project).
- `no-code-before-import`
  - Forbids any non-import code before last import expression.
  ```ts
  // Good:
  import module from 'module';
  fn();

  // Bad:
  fn();
  import module from 'module';
  ```
  - Rule option: `"ignore-dynamic-import"`. If enabled, ignores dynamic import call expressions.
  - This rule has a fixer though it is not aware of indentations in the project.
    Dynamic imports will be transported in the beginning of the file with the top source file expression that includes them.
- `no-default-as-import`
  - Forbids imports with default syntax.
  ```ts
  // Good:
  import module from 'module';

  // Bad:
  import {deafult as module) from 'module';
  ```
  - This rule has a fixer.
- `no-inline-export`
  - Forbids any inline export expression except the ones with identifier for all files and the ones with class, function or variable for declaration files (by default).
  ```ts
  // Good:
  export default utils;
  export {utils};

  // Bad:
  export default const a = true;
  export type A = boolean;
  ```
  - Rule options: `["CallExpression", "TypeAliasDefinition", ...]`. Kinds of expressions included in the option will be allowed as inline export.
    Complete list of aliases can be found [in typescript library typings](https://github.com/Microsoft/TypeScript/blob/master/lib/typescript.d.ts#L64).
  - This rule has a fixer for limited amount of expressions, e.g. anonymous function default export cannot be fixed.
- `no-jsx-attribute-bind-function`
  - Forbids any usage of bind function as an JSX attribute.
  ```ts
  // Good:
  <div fn={() => some.deep.fn(arg)} />

  // Bad:
  <div fn={some.deep.fn.bind(this, arg)} />
  ```
  - This rule has a fixer, but beware that it does remove the first argument of the bind function (usually this) completely and doesn't have any knowledge about previously-omitted function arguments.
- `no-jsx-boolean-and-shorthand`
  - Forbids imports with default syntax.
  ```ts
  // Good:
  <div>
    {foo ? bar : null}
  </div>

  // Bad:
  <div>
    {foo && bar}
  </div>
  ```
  - This rule has a fixer.
- `prefer-includes`
  - Forbids indexOf / lastIndexOf when includes / startsWith can be used.
  ```ts
  // Good:
  foo.includes(bar)
  foo.startsWith(bar)

  // Bad:
  foo.indexOf(bar) === -1
  foo.indexOf(bar) !== -1
  ```
  - This rule has a partial fixer.
- `react-forbid-default-props`
  - Forbid defaultProps in React components.
  ```ts
  // Good:
  class Foo extends React.Component {}
  
  // Bad:
  class Foo extends React.Component {
    static defaultProps = {x: 1}
  }
  Bar.defaultProps = {x: 1};
  ```
- `return-value-typed`
  - Enforces types for return values in top-level classes / top-level functions / default export functions.
  ```ts
  // Good:
  const fooUtils = {
    bar: (): boolean => {
      ...
    }
  }
  
  // Bad:
  const fooUtils = {
    bar: () => {
      ...
    }
  }
  ```
  - Rule options: `["default-export-object", "top-level-function", "top-level-class"]`.

### Contributing

To test package rules run
```
npm test
```
To test rule locally run `npm run build`, copy build folder to `/your-project/my-custom-folder` and add `"rulesDirectory": "./my-custom-folder"` to your tslint.json config.

Custom rule development process is described on [TSLint website](https://palantir.github.io/tslint/develop/custom-rules/).
