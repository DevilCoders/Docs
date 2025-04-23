# @yandex-int/edu-stylelint

![npm version](https://badger.yandex-team.ru/npm/@yandex-int/edu-stylelint/version.svg)
![npm owners](https://badger.yandex-team.ru/npm/@yandex-int/edu-stylelint/owner.svg)

Пакет с линтером Stylelint и конфигурационным файлом для него. Предназначен для использования вместе с [Prettier](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-prettier).

## Установка

```sh
npm install --save-dev @yandex-int/edu-stylelint @yandex-int/edu-prettier
```

## Настройка

Создайте конфигурационный файл с названием `.stylelintrc.js` в корне вашего проекта и вставьте следующее содержимое:

```js
const eduStylelintConfig = require('@yandex-int/edu-stylelint');

module.exports = {
  ...eduStylelintConfig,
};
```

Также создайте файл `.stylelintignore` в корне и перечислите все директории и файлы, которые не нужно форматировать:

```
build/
```

_Важно: на данный момент Stylelint не умеет рекурсивно подтягивать содержимое файлов .stylelintignore в поддиректориях. Работа ведётся в тикете [FRONTEND-360](https://st.yandex-team.ru/FRONTEND-360)._

Для корректной работы с Prettier нужно настроить его по [инструкции](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-prettier#%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0).

## Миграция

Отформатируйте существующие стили:

```sh
npx prettier --write "**/*.css"
```

Почините автоматически то, что возможно:

```sh
npx stylelint --fix "**/*.css"
```

Оставшиеся ошибки обработайте вручную следуя инструкциям линтера.

## Использование

Stylelint поддерживается в IDE через плагины:

- [Для Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=thibaudcolas.stylelint)

Для JetBrains IDE (WebStorm, IDEA, etc) устанавливать ничего не нужно, плагин вшит в комплект поставки и включен по умолчанию.

Возможно также использование через CLI:

```sh
stylelint '**/*.css'
stylelint --fix '**/*.css'
```

Команды можно записать в секцию `scripts` файла `package.json`:

```json
{
  "private": true,
  "name": "@yandex-int/your-service",
  "scripts": {
    "tools:stylelint": "stylelint '**/*.css'",
    "tools:stylelint-fix": "stylelint --fix '**/*.css'"
  },
  "devDependencies": {
    "@yandex-int/edu-prettier": "1.0.0",
    "@yandex-int/edu-stylelint": "1.0.0"
  }
}
```

И вызывать через `npm run`:

```sh
npm run tools:stylelint
npm run tools:stylelint-fix
```

## TODO

- Дождаться возможности расширения `@yandex-int/lint` своими модулями и добавить `stylelint-config-prettier`, `stylelint-prettier`
- Подождать закрытия [бага в плагине](https://github.com/stylelint/vscode-stylelint/issues/4) Stylelint для VSCode и обновить пакеты `stylelint` и `stylelint-config-prettier`
