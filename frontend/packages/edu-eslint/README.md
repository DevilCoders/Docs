# @yandex-int/edu-eslint

![npm version](https://badger.yandex-team.ru/npm/@yandex-int/edu-eslint/version.svg)
![npm owners](https://badger.yandex-team.ru/npm/@yandex-int/edu-eslint/owner.svg)

Пакет с линтером ESLint и конфигурационным файлом для него. Предназначен для использования вместе с [Prettier](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-prettier).

## Установка

```sh
npm install --save-dev @yandex-int/edu-eslint @yandex-int/edu-prettier
```

## Настройка

Создайте конфигурационный файл с названием `.eslintrc.js` в корне вашего проекта и вставьте следующее содержимое:

```js
const eduEslintConfig = require('@yandex-int/edu-eslint');

module.exports = {
  ...eduEslintConfig,
};
```

Также создайте файл `.eslintignore` в корне и перечислите все директории и файлы, которые не нужно форматировать:

```
build/
```

_Важно: на данный момент ESLint не умеет рекурсивно подтягивать содержимое файлов .eslintignore в поддиректориях. Работа ведётся в тикете [FRONTEND-280](https://st.yandex-team.ru/FRONTEND-280)._

Для корректной работы с Prettier нужно настроить его по [инструкции](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-prettier#%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0).

## Миграция

Отформатируйте существующий код:

```sh
npx prettier --write "**/*.{js,jsx,ts,tsx}"
```

Почините автоматически то, что возможно:

```sh
npx eslint --fix "**/*.{js,jsx,ts,tsx}"
```

Оставшиеся ошибки обработайте вручную следуя инструкциям линтера.

## Использование

ESLint поддерживается в IDE через плагины:

- [Для Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

Для JetBrains IDE (WebStorm, IDEA, etc) устанавливать ничего не нужно, плагин вшит в комплект поставки и включен по умолчанию.

Возможно также использование через CLI:

```sh
eslint '**/*.{js,jsx,ts,tsx}'
eslint --fix '**/*.{js,jsx,ts,tsx}'
```

Команды можно записать в секцию `scripts` файла `package.json`:

```json
{
  "private": true,
  "name": "@yandex-int/your-service",
  "scripts": {
    "tools:eslint": "eslint '**/*.{js,jsx,ts,tsx}'",
    "tools:eslint-fix": "eslint --fix '**/*.{js,jsx,ts,tsx}'"
  },
  "devDependencies": {
    "@yandex-int/edu-eslint": "*",
    "@yandex-int/edu-prettier": "*"
  }
}
```

И вызывать через `npm run`:

```sh
npm run tools:eslint
npm run tools:eslint-fix
```
