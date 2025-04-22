
# MandrelLayer

Слой для работы с контекстом

## Методы слоя

### Constructor
`constructor(config?: Config)`

- `config.resourcesPath: string` - путь как директории с ресурсами
- `config.envConfig: object` - карта бекендов и их хостов
- `config.showResourceLog?: boolean` - показывать логи ресурсов (по умолчанию `false`)
- `config.defaultRoutes?: object` - дефолтные роуты для роутера (стандартный формат сусанина)

```js
const mirror = new Mirror(); // создать mirror
const mandrelLayer = new MandrelLayer({
    resourcesPath: path.dirname(require.resolve('@self/platform/app/resource')),
    envConfig: require('@self/platform/configs/current/node').servant,
});
```

Или c помощью [хелпера](../helpers.md)

```js
mirror = await makeMirror({
    jest: { // это будет передано в конструктор
        testFilename: __filename,
        jestObject: jest,
    }
});
mandrelLayer = mirror.getLayer('mandrel');
```

в Хелпере в makeMirror нет необходимости подавать resourcePath или envConfig, потому что,
это происходит под капотом:
```js
const mandrelConfig = {
    resourcesPath: path.dirname(require.resolve('@self/platform/app/resource')),
    envConfig: require('@self/platform/configs/current/node').servant,
    ...config.mandrel,
};
```

### initContext
`initContext(params?: InitContextArg): Promise<Context | null>`

Создать mandrel-контекст, в качестве параметра принимает объект, в котором можно описать настройки контеста (например, симулировать участие в эксперименте или задать любые настройки пользователя)

- `params?` - параметры контекста ([InitContextArg](
  https://a.yandex-team.ru/arc_vcs/market/front/libs/testament/src/mirror/layers/mandrel/contextHelpers.ts#L74))
```ts
export type InitContextArg = {
    route?: InitRouteArg;
    user?: InitUserArg;
    request?: InitRequestArg;
    page?: any;
};
```

Пример инициализации контекста

```js
await mandrelLayer.initContext({
    user: {
        UID,
        yandexuid,
        settings,
    },
    request: {
        cookie,
        abt: {
            expFlags: exps
        },
        params: {
            productId,
        },
    },
    route: {
        name: pageId
    },
    page: {
        pageId,
    }
});
```

Можно вызывать `initContext` и без параметров, это создаст полное фейковое окружение, главное условие - **initContext нужно вызывать в каждом тесте!**
