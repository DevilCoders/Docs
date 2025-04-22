# eslint-plugin-i18n

Linter for cyrillic chars not wrapped in i18n call

## Installation

You'll first need to install [ESLint](https://eslint.org/):

```sh
npm i eslint --save-dev
```

Next, install `@yandex-id/eslint-plugin-i18n`:

```sh
npm install @yandex-id/eslint-plugin-i18n --save-dev
```

## Usage

Add `i18n` to the plugins section of your `.eslintrc` configuration file. You can omit the `eslint-plugin-` prefix:

```json
{
    "plugins": [
        "@yandex-id/i18n"
    ]
}
```


Then configure the rules you want to use under the rules section.

```json
{
    "rules": {
        "@yandex-id/i18n/no-unwrapped-strings": 2
    }
}
```

## Supported Rules

* [no-unwrapped-strings](docs/rules/no-unwrapped-strings.md)
