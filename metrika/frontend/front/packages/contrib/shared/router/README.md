Утилита для создания расширяемого роутера. За базовые тайпинги страницы взят react-router

Примеры использования:

1. Можно передать массив для создания роутера
```
    const router = createRouter([
        { id: 'first', path: '/first' },
        { id: 'second', path: '/second' },
    ]);
```
2. Либо добавлять страницы по отдельности.
```
    const router = createRouter()
        .addRoute({ id: 'first', path: '/first'})
        .addRoute(
            { id: 'second', path: '/second'},
            { id: 'third', path: '/third'},
        )
```
3. Базовый набор свойств можно расширить при необходимости
```
    const expressRouter = router.extend<{ middlewares: Middleware[]}>({
        first: { middlewares: [middleware1] },
        second: { middlewares: [middleware1, middleware2] },
    });

    console.log(expressRouter.get());
    // OUTPUT [{ id: 'first', path: '/first', middlewares: [middleware1]}, ...pages]
```
4. Можно ограничить список страниц, если в каком то месте используется только их часть.
```
    const router2 = router.only(['first', 'second']);
```
5. Можно получить итоговый массив страниц
```
    const routes = router.get();

    console.log(routes);
    // OUTPUTP [{ id: 'first', path: '/first', ...other }, ...pages]
```