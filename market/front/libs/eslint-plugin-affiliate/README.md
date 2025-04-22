# eslint-plugin-affiliate

Simple plugin implement sort import specifiers by natural sort oder ([wiki](https://en.wikipedia.org/wiki/Natural_sort_order)), with autofix and without format code style.

## Installation

You'll first need to install [ESLint](http://eslint.org):

```
$ npm i eslint --save-dev
```

Next, install `eslint-plugin-affiliate`:

```
$ npm install git://github.yandex-team.ru/moonw1nd/eslint-plugin-affiliate.git#0.0.1 --save-dev
```

**Note:** If you installed ESLint globally (using the `-g` flag) then you must also install `eslint-plugin-affiliate` globally.

## Usage

Add `affiliate` to the plugins section of your `.eslintrc` configuration file. You can omit the `eslint-plugin-` prefix:

```json
{
    "plugins": [
        "affiliate"
    ]
}
```


Then configure the rules you want to use under the rules section.

```json
{
    "rules": {
        "affiliate/rule-name": 2
    }
}
```

## Supported Rules

* [sort-import-specifiers](./docs/rules/sort-import-specifiers.md)





