# `@vertis/package-lock-checker`

Проверяет package-lock.json на:
1) Поля "resolved" ведут на `http(s)://npm.yandex-team.ru`
2) "lockfileVersion" 2 (npm v7), а не версии 1 (npm v6)

## Installation

```
$ npm install --registry=https://npm.yandex-team.ru --save-dev @vertis/package-lock-checker
```

## Usage

```
$ npx check-package-lock ./package-lock.json
```

**lint-staged**
```
{
    "package-lock.json": "npx check-package-lock"
}
```
