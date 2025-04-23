# Admin-Front

## Подготовка
Для работы потребуется Node.js 12.16.1.

Для локальной разработки мы используем [NVM](https://github.com/nvm-sh/nvm).

Устанавливаем NVM, а затем:
```bash
# Устанавливаем Node.js 12.16.1 версии
nvm install 12.16.1

# Переключаемся на эту версию
nvm use 12.16.1
```

## Настройка проекта

```bash
# установить зависимости
npm ci
```

## Запуск

```bash
npm start
```

Смотреть после запуска тут: [http://localhost:3000/](http://localhost:3000/).

The page will reload if you make edits.<br />
You will also see any lint errors in the console.

### Tests

[Jest](https://jestjs.io/docs/en/api) and [Enzyme](https://airbnb.io/enzyme/docs/api/) are used for testing.

To run local tests, use:

```shell
npm run test
```

## Environment variables

| Environment variable      | Example                                         | Description                            |
| ------------------------- | ----------------------------------------------- | ---------------------------------------|
| BROWSER                   | none                                            | Browser to open after starting the app |
| PORT                      | 3000                                            | Development server port bind           |

## Contributing

We are using [Create React App](https://create-react-app.dev) with [TypeScript](https://www.typescriptlang.org).

### Templating

We are using using [hygen](http://www.hygen.io) for code generation.

#### Generating a component

```shell
npm run generate component new <newComponentName>
```

This command will create a new React component at `src/components`
path with a starting set of files.

Component templates are located in `_templates/component/new`.

### Naming Convention

#### Actions

Actions, that are part of some module, must have a type, prefixed with the name of that module.
Action types must be named in form of `<NOUN>_<VERB>`. Note, that the verb must be in the past tense as the action should be interpreted as an accomplished fact. If the action is intent, it should be made clear with some suffix, eg. `_REQUESTED`.

```js
export const MENU_OPENED = '@@ui/MENU_OPENED';
export const MENU_CLOSED = '@@ui/MENU_CLOSED';
```

Async actions must form a triplet  — a request, and two possible outcomes — success and failure.

```js
export const AUTH_REQUESTED = '@@user/AUTH_REQUESTED';
export const AUTH_SUCCEEDED = '@@user/AUTH_SUCCEEDED';
export const AUTH_FAILED = '@@user/AUTH_FAILED';
```

#### Selectors

Selectors must be named in the form of `get<NOUN>`.

```js
export const getMenuIsOpen = createSelector(
  uiSelector,
  (ui) => ui.menuIsOpen
);
```

### Interfaces vs. Type Aliases

Prefer Type Aliases over Interfaces.

### Commit messages

We are using [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) specification for commit messages.

```text
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```
