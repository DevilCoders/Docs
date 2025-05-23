# Асинхронные редюсеры

Редюсеры, которые попадают в бандл страницы, на которой используются, а не в общий бандл.

## Проблематика

В стандартной реализации, все редюсеры импортируются напрямую в файле с рутовым редюсером или в файле с вложенным редюсером. При таком подходе все редюсеры оказываются в одном бандле с рутовым редюсером. И чем больше у нас новых страниц, чем больше мы храним данных в редаксе, тем сильней раздувается общий бандл.

## Решение

В самом редюсере использовать не чистые функции редюсеры, а обертку `loadableReducer`, которая приминает в качестве аргумента ключ редюсера, что помогает идентифицировать редюсер позже.

![loadableReducer](./loadableReducer.png)

Затем подгружать необходимые для компонента редюсеры в обертке `withReducer`, которая принимает на вход массив с подмассивом: ключ редюсера и сам редюсер.

![withReducers](./withReducers.png)

![ELoadableReducer](./ELoadableReducer.png)

В такой конфигурации редюсеры будут приходить в бандле с компонентом и прямо перед первым рендером подключаться в общий стор и инициализироваться.
