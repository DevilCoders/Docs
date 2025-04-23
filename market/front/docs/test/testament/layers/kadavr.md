# KadavrLayer

Слой для работы с кадавром.

> Кадаврик — приложение, реализующее отдачу фиктивных данных для интеграционных функциональных автотестов сервисов Маркета. Главная задача — обеспечение стабильного тестового окружения.

## Методы

### constructor
`constructor(config: Config)`

- `config.host: string` - хост, на котором поднят кадавр
- `config.port: number` - порт, на котором поднят кадавр
- `config.asLibrary: boolean` - устаревшее, сейчас включено в true по дефолту

Пример

```js
const mirror = new Mirror();
const kadavrLayer = new KadavrLayer({
    host: 'kadavr2.vs.market.yandex.net',
    port: 80,
});
```

Или c помощью [хелпера](../helpers.md) - в коде Маркета применяется именно такой подход (но под капотом там будет пример выше):

```js
mirror = await makeMirror({
        jest: {
            testFilename: __filename,
            jestObject: jest,
        }
    });
kadavrLayer = mirror.getLayer('kadavr');
```

Для того чтобы хелпер не создавал слой kadavr, нужно указать параметр skipLayer:

```js
mirror = await makeMirror({
        jest: {
            testFilename: __filename,
            jestObject: jest,
        },
        kadavr: {
            skipLayer: true, // не ининциализировать слой кадавра
        },
    });
jestLayer = mirror.getLayer('jest');
mandrelLayer = mirror.getLayer('mandrel');
apiaryLayer = mirror.getLayer('apiary');
// кадавра тут нет
```

{% note warning %}

Принятым на уровне конвенций, считается способ с использованием kadavrLayer

{% endnote %}

### getSessionId

`getSessionId(): string | null`

Получить ID сессии кадавра. Обычно сессию закидываем в куки. Можно сделать это так:

```js
await mandrelLayer.initContext({
    request: {
        cookie: {
            kadavr_session_id: await kadavrLayer.getSessionId()
        },
    },
});
```

{% note warning %}

Для работы кадавра как библиотеки кука необходима!
`kadavr_session_id: await kadavrLayer.getSessionId()`
Устанавливается кука в слое мандреля.

{% endnote %}

### setState

`setState<TData>(path: string, data: TData): Promise<void>`

Установить kadavr-стейт

- `path` - путь стейта
- `data` - данные для стейта

Работает так же, как в случае с тестами на гермионе

```js
await kadavrLayer.setState('report', reportState);
```

Все существующие моки в кадавре можно [посмотреть в коде](
https://a.yandex-team.ru/arc_vcs/market/front/apps/kadavrique/options/mocks.js
).

Как видно, достаточно много эндпоинтов покрыто кадавром, если понадобится писать новые,
то скорее всего для этого уже есть созданный класс.
Если есть необходимость написать свой мок, то самый простой мок на кадавре выглядит так:
```js
class FooMock extends Mock {
    foo() {
        return this.state.get('FooMock.someData');
    }
}
```
А со стороны теста будет так:
```js
await kadavrLayer.setState('FooMock.someData', {...})
```

### Как определить нужный ресурс
1. Используемый ресур можно увидеть в логах на логрусе, например <persAuthor.getExpertiseDictionary>.
2. Делаем поиск в проекте по названию ресурса (getExpertiseDictionary)
    ```js
    export const fetchExpertiseDictionary = method<Method>({
        pathname: '/expertise/dictionary',
        name: 'getExpertiseDictionary',
        ...
    });
    ```
3. Достаем pathname
4. Вбиваем в поиск в моках кадаврика в аркануме [market/front/apps/kadavrique](
   https://a.yandex-team.ru/arc_vcs/market/front/apps/kadavrique/options/mocks.js
   ).
5. Если находим нужный, то используем его. Если не находим, то добавляем новый мок в кадаврик.

Ну и ссылочка на [доку](https://wiki.yandex-team.ru/market/verstka/kadavrcookbook/) по кадавру.

[Пример моков кадавра](../mocks.md#moki-urovnya-kadavrlayer)
