# `lib/dispatch`

Redux-like система middleware для отправки событий.

Здесь находится ядро dispatch'а в виде класса `Dispatcher`.
Экземпляр dispatcher'а может быть получен через [инжектор](../inject/) как
```typescript
class MyService {
    static Token = SingletonToken(MyService, {
        dispatcher: Dispatcher.Token()
    });

    constructor(private params: { dispatcher: Dispatcher }) {
    }

    public async doSomeStuff() {
        await this.params.dispatcher.dispatch(new SomeAction());
    }
}
```

> `Dispatcher` не содержит никакой логики обработки конкретных типов action'ов.
Вся логика задаётся набором middlewares, переданным в метод `registerMiddlewares()`.
Конкретный middleware, поддерживаемые `react-client`'ом можно найти в директории [lib/middleware](../middleware/).
