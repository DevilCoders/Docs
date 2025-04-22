# uatraits

uatraits (User Agent traits)

Nest обертка над `@yandex-int/express-http-uatraits`

Экспортирует:

```ts
export {
    UatraitsModule, // Модуль
    UatraitsService, // Сервис
    UatraitsOptions, // Тайпинги конфига
    Uatraits, // Тайпинги uatraits данных
};
```

## UatraitsModule

Экспортирует сервис `UatraitsService`

Подключается в `appModule` единожды и для работы необходим `AsyncStorageModule`

```ts
import { Module } from '@nestjs/common';
import { AsyncStorageModule } from '@yandex-int/nest-common';
import { UatraitsModule } from '@yandex-int/nest-infra';

@Module({
    imports: [
        UatraitsModule.forRoot(/* UatraitsOptions */),
        // или если использовать дефолтные настройки
        // UatraitsModule
        AsyncStorageModule.forRoot(),
    ],
})
export class ApiModule {}
```

## UatraitsService

Может запросить tvm тикеты методом `.getUatraits()`

```ts
import { UatraitsService } from '@yandex-int/nest-infra';

export class SomeService {
  constructor(private uatraitsService: UatraitsService) {}

  async method () => {
    const uatraits = await uatraitsService.getUatraits();
  }
}
```

## UatraitsOptions

```ts
type UatraitsOptions = {
    /**
     * Адрес http-uatraits API server
     *
     * Default: 'http://uatraits.qloud.yandex.ru'
     *
     * Для local, develop, testing 'http://uatraits-test.qloud.yandex.ru'
     * Для production 'http://uatraits.qloud.yandex.ru'
     */
    server?: string;

    /**
     * TODO
     *
     * Если не знаешь что ставить - пропиши
     * {
     *    timeout: 100
     * }
     */
    clientOptions?: {
        body?: string | Buffer | Readable | object;
        encoding?: string | null;
        json?: boolean;
        query?: string | object;
        timeout?: number | object;
        retries?: number | ((retryCount: number, error: Error) => void);
        followRedirect?: boolean;
    };
};
```
