# config

Цели:

-   конфиги должны быть изоморфными
-   максимально простое подключение (без babel/webpack магии)
-   поддержка разных окружений
-   разделение на приватную и публичную части
-   разделение по фичам (app, s3, blackbox и т.д.)
-   возможность сделать сборку только конкретного окружения

## Быстрый старт

Например, раскладываем настройки приложения. Конфиги будем хранить в папке `src/config/`.

### Создаем файловую структуру

```
src/config/
├── app
│   ├── private.ts
│   └── public.ts
└── index.ts
```

```bash
mkdir -p src/config/app/
```

### Создаем экземпляр провайдера

Файл `src/config/index.ts`:

```ts
import {ConfigProvider, createEnvironmentGetter} from '@lavka-js-toolbox/config';

export const getEnv = createEnvironmentGetter('NODE_ENV'); // из какой переменной получаем окружение
export const config = new ConfigProvider();
```

### Создаем публичные настройки

Файл `src/config/app/public.ts`:

```ts
import {config, getEnv} from '..';

export type Public = {
    name: string;
    version: string;
    domain: string;
};

export default config
    .section<Public>()
    .set('development', {
        name: 'development_name',
        version: 'development_version',
        domain: 'development_domain'
    })
    .inherit('testing', (it) => {
        it.domain = 'testing_domain';
    })
    .inherit('production', (it) => {
        it.domain = 'production_domain';
    })
    .get(getEnv());
```

### Создаем приватные настройки

Файл `src/config/app/private.ts`:

```ts
import {config, getEnv} from '..';
import publicConfig, {Public} from './public';

type Private = Public & {
    secret: string;
};

export default config
    .section<Private>()
    // осторожно, publicConfig уже привязан к текущему окружению =)
    .set('development', {...publicConfig, secret: 'development_secret'})
    .inherit('testing', (it) => {
        it.secret = 'testing_secret';
    })
    .inherit('production', (it) => {
        it.secret = 'production_secret';
    })
    .get(getEnv());
```

## API

### ConfigProvider.bootstrap

Можно передать асинхронный загрузчик:

```ts
const config = new ConfigProvider<Environment, {ok: boolean}>({
    bootstrap: new Promise((resolve) => {
        setTimeout(() => resolve({ok: true}), 100);
    })
});
await config.ready;
config.getBootstrap(); // {ok: true}
```

### SectionProvider.set

Устанавливаем значение для окружения:

```ts
config.section<{foo: string}>().set('testing', {foo: 'bar'}).get('testing'); // {foo: 'bar'}
```

### SectionProvider.setFrom

Устанавливаем значение для окружения используя другое окружение:

```ts
config
    .section<{foo: string}>()
    .set('testing', {foo: 'bar'})
    .setFrom('production', 'testing', (draft) => {
        draft.foo = 'baz';
    })
    .get('production'); // {foo: 'baz'}
```

### SectionProvider.inherit

Устанавливаем значение для окружения используя предыдущее окружение:

```ts
config
    .section<{foo: string}>()
    .set('testing', {foo: 'bar'})
    .inherit('production', (draft) => {
        draft.foo = 'baz';
    })
    .get('production'); // {foo: 'baz'}
```
