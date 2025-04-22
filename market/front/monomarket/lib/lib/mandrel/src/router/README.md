Роутер

В страничный виджет подключаем редьюсер для "коллекции" route (`makeLocationReducer`), в него передаем функцию, которая будет превращать [RouteSpec](https://github.yandex-team.ru/market/mandrel/blob/master/src/router/index.js) в href-ы

Размечаем слоты компонентом Route, с нужным pageId:
```javascript
<Route pageId="touch:product">
  // path a
</Route>
<Route pageId="touch:product-filters">
  // path b
</Route>
```
Для скрытия частей страницы необходимо подключить редьюсер hideParts передавать partsToHide:
```javascript
<Route pageId="touch:product" partsToHide={{header: true}} >
  
</Route>
```

Точки переходов в СПА реализованы компонентом Link, которому в route кладем RouteSpec роута, на которой необходимо перейти, и передаем строющую href функцию.

