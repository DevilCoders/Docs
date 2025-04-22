# Стор
Для храннения данных приложения используется redux, в частности утилиты:
* [react-redux](https://react-redux.js.org/)
* [redux-toolkit](https://redux-toolkit.js.org/)

Реализация логики изменения состояния инкапсулирована внутри одного файла, который содержит как
экшены (actions), так и редьюсеры (reducers).

Асинхронные запросы за данными описываем внутри функций, которые лежат рядом с экшенами и редьюсерами.
Пример организации стейта:
https://redux-toolkit.js.org/tutorials/advanced-tutorial#logic-for-fetching-issues-for-a-repo
