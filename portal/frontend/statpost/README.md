# statpost

Класс для добавления данных в `statface`

## Пример использования

```js
const Statpost = require('statpost');

// Для авторизации по логину/паролю
const statpost = new Statpost({
    betaInstance: true, // Если хотим пушить данные на stat-beta.yandex-team.ru
    username: 'robot-username', // Имя робота, который добавляет данные
    password: 'robot-password' // Пароль для робота
});

// Для авторизации через OAuth
const statpost = new Statpost({
    betaInstance: true, // Если хотим пушить данные на stat-beta.yandex-team.ru
    authToken: 'statface-oauth-token' // Oauth токен робота
});

...

statpost.reportData(name, data) // имя измерения и значения
    .then(result => {
        console.log(result);
    })
    .catch(err => {
        console.log(err);
    });
```
