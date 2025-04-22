# yandex-y-cookie

Node.js модуль для работы с [Y-кукой](https://wiki.yandex-team.ru/Cookies/y/)

## Установка

```
npm install --registry=http://npm.yandex-team.ru yandex-y-cookie
```

## API

### parseYpCookie

```ts
interface YpSubcookies {
    [name: string]: {
        value: string,
        expire: Date
    }
}

function parseYpCookie(cookie: string): YpSubcookies
```

Разбирает перманентную куку `yp`.

## Запуск тестов

```
npm i
npm test
```
