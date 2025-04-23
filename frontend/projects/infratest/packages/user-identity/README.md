# user-identity

Плагин для [hermione](https://github.com/gemini-testing/hermione).
Добавляет в браузеры инструментов информацию о пользователе, который запускает тесты.

## Установка

```bash
npm install @yandex-int/user-identity --save-dev --registry https://npm.yandex-team.ru
```

## Подключение

Плагин имеет следующие опции:
- **enabled** (optional) `Boolean` – включает/выключает плагин. По умолчанию плагин включен; enable/disable the plugin;
- **browsers** (optional) `Regexp` - браузеры в которые необходимо добавить дополнительную информацию о запуске. По умолчанию матчится на все браузеры.

```js
plugins: {
    '@yandex-int/user-identity': {
        enabled: true, // by default
        browsers: /.*/ // by default
    }
}
```
