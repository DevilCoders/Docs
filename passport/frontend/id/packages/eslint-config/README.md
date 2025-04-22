# @yandex-id/eslint-config

Пакет c конфигурацией ESLint, которая используется на сервисах [Яндекс.ID](https://passport.yandex.ru/).

## Установка

Для начала установите необходимые зависимости:

```bash
npm i -DE eslint@8 @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-prettier eslint-import-resolver-typescript eslint-plugin-ascii eslint-plugin-import eslint-plugin-prettier eslint-plugin-react eslint-plugin-react-hooks
```

Установите пакет конфигурации:

```bash
npm i -DE @yandex-id/eslint-config
```

## Конфигурация

Создайте в корне репозитория файл конфигурации `.eslintrc.js` со следующим содержимым:

```js
module.exports = {
  root: true,
  extends: ['@yandex-id'],
};
```

Если у вас монорепозиторий, то для каждого пакета также необходимо установить `eslint`:

```bash
npm i -DE eslint@8
```

В `package.json` достаточно добавить скрипт:

```json
{
  "scripts": {
    "ci:lint": "eslint ."
  }
}
```

`ESLint` сам подтянет конфигурацию из корня монорепозитория. Подробнее можно узнать в [документации](https://eslint.org/docs/user-guide/configuring/configuration-files#cascading-and-hierarchy).

Чтобы добавить или переопределить правила на уровне пакета в монорепозитории, достаточно создать файл `.eslintrc.js`.

```js
module.exports = {
  rules: {
    'import/no-cycle': 'off',
  },
};
```

> Примечание:
>
> - наследовать конфигурацию для пакетов монорепозитория через `extends: ["@yandex-id"],` нет необходимости.
> - установку других конфигураций или плагинов eslint необходимо добавлять в корень монорепозиторий.
