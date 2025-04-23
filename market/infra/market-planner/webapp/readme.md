# Общие сведения

Фронтэнд Планнера — это только клиентская сборка. Клиентские бандлы собираются при помощи Webpack. В основе используется React, стейт-менеджер — Reatom. Для стилизации используется postcss через css modules. Общие ui-компоненты и стайлгайд — Levitan b2b. Типы — TypeScript.

## Как запустить фронт

Фронт лежит в папке webpapp. Для того, чтобы запустить фронт, нужно выполнить следующее:

```bash
# выбираем нужную версию ноды
nvm use 16
# ставим необходимые пакеты, требуется выполнять, если изменился package.json
npm i

# для запуска в связке с бэкендом
npm start

# для запуска на моках
MOCK_CLIENT=1 npm start
```
Открываем тут - http://localhost:3000

------
PS. можно не вызывать каждый раз `nvm use`, если установить дефолтную версию ноды:
```bash
nvm install 16
nvm alias default 16
```

## Сборка

```bash
nvm use 16
npm ci
npm run build
```

## Стоит почитать

- [Reatom](https://reatom.js.org/)
- [TypeScript](https://www.typescriptlang.org/)
- [Levitan b2b](https://levitan.yandex-team.ru/b2b/develop/core/)
- [Тикет по фронту Планнера](https://st.yandex-team.ru/MARKETQPLANNER-347/)
- [React](https://reactjs.org/)
- [Webpack](https://webpack.js.org/)

## e2e тесты

Для запуска тестов

1. Выполнить `npm run selenium`, эта команда установит и запустит `selenium`
2. Выполнить `npm run test:hermione`, это команда запустит тесты

