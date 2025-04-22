# @yandex-int/edu-prettier

![npm version](https://badger.yandex-team.ru/npm/@yandex-int/edu-prettier/version.svg)
![npm owners](https://badger.yandex-team.ru/npm/@yandex-int/edu-prettier/owner.svg)

Пакет с форматером кода Prettier и конфигурационным файлом для него. Prettier позволяет форматировать код на JavaScript, TypeScript, HTML, CSS, SCSS, JSON, YAML, Markdown и многих других языках.

## Установка

```sh
npm install --save-dev @yandex-int/edu-prettier
```

## Настройка

Создайте конфигурационный файл с названием `.prettierrc.js` в корне вашего проекта и вставьте следующее содержимое:

```js
const eduPrettierConfig = require('@yandex-int/edu-prettier');

module.exports = {
  ...eduPrettierConfig,
};
```

Также создайте файл `.prettierignore` в корне и перечислите все директории и файлы, которые не нужно форматировать:

```
node_modules/
package.json
package-lock.json
```

_Важно: на данный момент Prettier не умеет рекурсивно подтягивать содержимое файлов .prettierignore в поддиректориях. Работа ведётся в тикете [#4081 на GitHub](https://github.com/prettier/prettier/issues/4081)._

Рекомендуется также добавить файл `.editorconfig` с настройками EditorConfig, чтобы Prettier форматировал код с их учётом:

```editorconfig
root = true

[*]
charset = utf-8
indent_size = 2
indent_style = space
end_of_line = lf
max_line_length = 100
insert_final_newline = true
trim_trailing_whitespace = true

[*.md]
trim_trailing_whitespace = false
```

## Миграция

Отформатируйте вашу кодовую базу с помощью команды:

```sh
npx prettier --write "**/*.{ts,tsx,js,jsx,html,css,scss,json,yaml,yml,md}"
```

_Внимание: Это опасная операция, закомитьте все изменения перед её выполнением._

## Использование

Prettier поддерживается в IDE через плагины:

- [Для JetBrains IDE (WebStorm, IDEA, etc)](https://plugins.jetbrains.com/plugin/10456-prettier) (включен по умолчанию в WebStorm)
- [Для Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

Для комфортной работы можно сделать его форматером по умолчанию и применять в процессе написания кода.

Возможно также использование через CLI:

```sh
prettier --write '**/*.{js,jsx,ts,tsx,css,json,yaml,yml,md}'
```

Команду можно записать в секцию `scripts` файла `package.json`:

```json
{
  "private": true,
  "name": "@yandex-int/your-service",
  "scripts": {
    "tools:format": "prettier --write '**/*.{js,jsx,ts,tsx,css,json,yaml,yml,md}'"
  },
  "devDependencies": {
    "@yandex-int/edu-prettier": "1.0.0"
  }
}
```

И вызывать через `npm run`:

```sh
npm run tools:format
```
