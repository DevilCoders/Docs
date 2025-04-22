# XForwardedForFix

NestJS обертка над [@yandex-int/express-x-forwarded-for-fix](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/express-x-forwarded-for-fix) в виде интерсептора

Экспортирует:

```ts
export {
  XForwardedForFixInterceptor, // Интерсептор
  XForwardedForFixOptions, // Тайпинги настроек
};
```

## XForwardedForFixInterceptor

Как и любой интерсептор можно подключить в 3 местах:

Метод:

```ts
import { Controller, Get, UseInterceptors } from '@nestjs/common';
import { XForwardedForFixInterceptor } from '@yandex-int/nest-infra';

@Controller('api')
export class ApiController {
  @Get('get')
  @UseInterceptors(XForwardedForFixInterceptor)
  // Или если нужно указать конфиг
  // @UseInterceptors(new XForwardedForFixInterceptor(/* XForwardedForFixOptions */))
  async get() {
    ...
  }
}
```

Контроллер:

```ts
import { Controller, Get, UseInterceptors } from '@nestjs/common';
import { XForwardedForFixInterceptor } from '@yandex-int/nest-infra';

@Controller('api')
@UseInterceptors(XForwardedForFixInterceptor)
// Или если нужно указать конфиг
// @UseInterceptors(new XForwardedForFixInterceptor(/* XForwardedForFixOptions */))
export class ApiController {
  @Get('get')
  async get() {
    ...
  }
}
```

Глобально:

```ts
import { Module, APP_INTERCEPTOR } from '@nestjs/common';
import { XForwardedForFixInterceptor } from '@yandex-int/nest-infra';

@Module({
  providers: [
    {
      provide: APP_INTERCEPTOR,
      useClass: XForwardedForFixInterceptor,
      // Или если нужно указать конфиг
      // useValue: new XForwardedForFixInterceptor(/* XForwardedForFixOptions */),
    },
  ],
})
export class AppModule {}

// Так же можно через useGlobalInterceptors
app.useGlobalInterceptors(new XForwardedForFixInterceptor(/* XForwardedForFixOptions */));
```

## XForwardedForFixOptions

```ts
type ExpressXForwardedForFixOptions = {
  /**
   * Дефолтный ip если все остальные были профильтрованы
   *
   * Default: undefined
   */
  defaultIP?: string;

  /**
   * Убирать зарезервированные IP адреса
   *
   * Default: true
   */
  filterReserved?: boolean;

  /**
   * Позволяет разрешить подсети по маске (позволяет разрешить и адреса из зарезервированных)
   *
   * Default: []
   */
  allowedNetMasks?: Array<string | Netmask>;
};
```
