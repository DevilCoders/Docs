# Ticount Auth Plugin

Плагин ticount, проставляющий авторизационные куки паспорта для целевой страницы.

## Подключение 
- Устанавливаем npm пакет
```bash
npm i @yandex-int/ticount-auth-plugin --registry=http://npm.yandex-team.ru
```
- Добавляем в конфигурацию `ticount`
```js
// ticount.config.js

module.exports = {
    plugins: {
        beforePageOpening: [
            [
                '@yandex-int/ticount-auth-plugin',
                {
                    env: process.env.ENV,
                    login: process.env.USER_LOGIN,
                    password: process.env.USER_PASSWORD
                }
            ]
        ]
    }
}
```
Плагин принимает следующие опции:
```ts
type TicountAuthPluginOptions = {
    env: 'production' | 'testing';
    login: string;
    password: string;
}
```
- Запускаем ticount
```bash
ENV=production|testing USER_LOGIN=<user_login> USER_PASSWORD=<user_password> ticount write --url <actual_url> --metrics-log <metrics_file_name>
```
