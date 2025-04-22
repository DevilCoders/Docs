# tvm

Nest обертка над `@yandex-int/express-tvm`

Экспортирует:

```ts
export {
    TvmModule, // Модуль
    TvmService, // Сервис
    TvmOptions, // Тайпинги конфига
    TvmResult, // Тайпинги данных, возвращаемых tvm
};
```

## TvmModule

Экспортирует сервис `TvmService`

Подключается в `appModule` единожды
Для работы необходим `AsyncStorageModule`

```ts
import { Module } from '@nestjs/common';
import { AsyncStorageModule } from '@yandex-int/nest-common';
import { TvmModule } from '@yandex-int/nest-infra';

@Module({
    imports: [
      TvmModule.forRoot(/* TvmOptions */)
      /*
        TvmModule.forRootAsync({
          imports: [ConfigModule],
          inject: [ConfigService],
          useFactory: (configService: ConfigService) => configService.config.tvm, // TvmOptions
        }),
      */
      AsyncStorageModule.forRoot(),
    ],
})
export class AppModule {}

// либо через forRootAsync, если необходимо инжектить конфиг

@Module({
    imports: [
      TvmModule.forRootAsync({
        imports: [ConfigModule],
        inject: [ConfigService],
        useFactory: (configService: ConfigService) => configService.config.tvm, // TvmOptions
      }),
    ],
})
export class AppModule {}
```

## TvmService

Может запросить tvm тикеты методом `.getTvm()`

```ts
import { TvmService } from '@yandex-int/nest-infra';

export class SomeService {
  constructor(private tvmService: TvmService) {}

  async method () => {
    const tmvResult = await tldService.getTvm();
  }
}
```
