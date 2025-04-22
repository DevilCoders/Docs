# Стор
Для храннения данных приложения используется redux, в частности утилиты:
* [react-redux](https://react-redux.js.org)
* [redux-toolkit](https://redux-toolkit.js.org/)

Асинхронные запросы за данными описываем внутри функций, которые лежат рядом с экшенами и редьюсерами.
Пример организации стейта:
https://redux-toolkit.js.org/tutorials/advanced-tutorial#logic-for-fetching-issues-for-a-repo

## Разработка

При любых изменениях внутри стейта необходимо изменить версию внутри конфига для `redux-persist` или написать соответствующую миграцию. Конфиг находится [здесь](./helpers/persist.ts).
