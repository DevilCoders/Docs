# Yandexuid

Nest обертка над `@yandex-int/express-yandexuid`

Экспортирует:

```ts
export {
    YandexuidModule, // Модуль
    YandexuidService, // Сервис
    YandexuidInterceptor, // Интерсептор
    YandexuidOptions, // Тайпинг настроек
};
```

## Зависимости

Для работы в любом виде необходим подключенный в appModule `UatraitsModule` и `AsyncStorageModule`

```ts
import { Module } from '@nestjs/common';
import { AsyncStorageModule } from '@yandex-int/nest-common';
import { UatraitsModule } from '@yandex-int/nest-infra';

@Module({
    imports: [UatraitsModule.forRoot(/* UatraitsOptions */), AsyncStorageModule.forRoot()],
})
export class ApiModule {}
```

## YandexuidModule

Модуль экспортирует сервис `YandexuidService` и интерсептор `YandexuidInterceptor`

## YandexuidService

Имеет 2 метода: `.getYandexuidCookie()` - возвращает объект

```ts
{
  uid: string, // сгенерированный uid
  cookieOptions: CookieOptions, // express cookie options. Настройки для express res.cookie
}
```

И `.getYandexuid()` - возвращает только uid из предыдущего метода

## YandexuidInterceptor

Генерирует и подсобывает в `Set-cookie` заголовок yandexuid

Может подключается как и любой интерсептор в 3 места

Метод:

```ts
import { Controller, Post, UseInterceptors } from '@nestjs/common';
import { YandexuidInterceptor } from '@yandex-int/nest-infra';

@Controller('api')
export class ApiController {
  @Post('create')
  @UseInterceptors(YandexuidInterceptor)
  async create() {
    ...
  }
}
```

Контроллер:

```ts
import { Controller, Post, UseInterceptors } from '@nestjs/common';
import { YandexuidInterceptor } from '@yandex-int/nest-infra';

@Controller('api')
@UseInterceptors(YandexuidInterceptor)
export class ApiController {
  @Post('create')
  async create() {
    ...
  }
}
```

Глобально:

```ts
import { Module, APP_INTERCEPTOR } from '@nestjs/common';
import { YandexuidModule, YandexuidInterceptor } from '@yandex-int/nest-infra';

@Module({
    imports: [
        YandexuidModule.register(/* YandexuidConfig */),
        // или если использовать настройки по-умолчанию
        // YandexuidModule,
    ],
    providers: [
        {
            provide: APP_INTERCEPTOR,
            useClass: YandexuidInterceptor,
        },
    ],
})
export class AppModule {}
```

При этом стоит помнить, что при использовании в контроллерах и методах необходимо в модуль контроллера / метода заимпортить `YandexuidModule`

```ts
import { Module } from '@nestjs/common';
import { YandexuidModule } from '@yandex-int/nest-infra';

// Если хотите использовать дефолтные настройки
@Module({
    imports: [YandexuidModule],
})
export class ApiModule {}

// Если хотите выставить настройки
@Module({
    imports: [YandexuidModule.register(/* YandexuidOptions */)],
})
export class ApiModule {}
```

Можно подключить `YandexuidModule` глобально:

```ts
import { Module } from '@nestjs/common';
import { YandexuidModule } from '@yandex-int/nest-infra';

// Если хотите выставить настройки
@Module({
    imports: [YandexuidModule.forRoot(/* YandexuidOptions */)],
})
export class ApiModule {}
```

## YandexuidOptions

```ts
type YandexuidOptions = {
    /**
     * Домен, на котором устанавливается кука.
     *
     * Default: '.yandex.{tld}' (`{tld}` — текущий top level domain)
     */
    yaDomain?: string;

    /**
     * Срок жизни куки.
     *
     * Default: + 10 лет от текущей даты
     * expires.setFullYear(expires.getFullYear() + 10)
     */
    expires?: Date;
};
```
