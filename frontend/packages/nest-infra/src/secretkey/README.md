# Secretkey

Nest обертка над `@yandex-int/express-secretkey`

Экспортирует:

```ts
export {
    SecretkeyModule, // Модуль
    SecretkeyService, // Сервис
    SecretkeyGuard, // Guard
    SecretkeyOptions, // Тайпинг настроек
};
```

## Зависимости

Для работы в любом виде необходим подключенные в appModule `BlackboxModule`, `YandexuidModule` и `AsyncStorageModule`

```ts
import { Module } from '@nestjs/common';
import { AsyncStorageModule } from '@yandex-int/nest-common';
import { BlackboxModule, YandexuidModule } from '@yandex-int/nest-infra';

@Module({
    imports: [
        BlackboxModule.forRoot(/* BlackboxOptions */),
        YandexuidModule.forRoot(/* YandexuidOptions */),
        AsyncStorageModule.forRoot(),
    ],
})
export class ApiModule {}
```

## SecretkeyModule

Модуль экспортирует сервис `SecretkeyService` и guard `SecretkeyGuard`

## SecretkeyService

Умеет 2 вещи: генерировать secretkey (`.getSecretkey()`) и валидировать пользователя (`.validate()`)

Классический сценарий использования этих методов:

1. Пользователь запрашивает страничку
2. Вместе со страничкой передаем `secretkey` на клиент

```ts
import { Controller, Get, Render } from '@nestjs/common';
import { SecretkeyService } from '@yandex-int/nest-infra';

@Controller('pages')
export class PageController {
    constructor(private secretkeyService: SecretkeyService) {}

    @Get()
    @Render('index')
    async get() {
        const secretkey = await this.secretkeyService.getSecretkey();

        return {
            secretkey,
        };
    }
}
```

3. Далее клиент при api запросах передает этот secretkey (допустим в хедере `csrf-token`)
4. В api ручке проверяем методом `.validate()`

```ts
import { Controller, Post, ForbiddenException } from '@nestjs/common';
import { SecretkeyService } from '@yandex-int/nest-infra';

@Controller('api')
export class ApiController {
  constructor(private secretkeyService: SecretkeyService) {}

  @Post('create')
  async create() {
    const isValid = await this.secretkeyService.validate();

    if (!isValid) {
      throw new ForbiddenException();
    }

    ...
  }
}
```

## SecretkeyGuard

Вместо проверки методом `secretkeyService.validate()` лучше воспользоваться `SecretkeyGuard` который сделает это за вас

Существует 3 места куда можно подключить `SecretkeyGuard`

Метод:

```ts
import { Controller, Post, UseGuards } from '@nestjs/common';
import { SecretkeyGuard } from '@yandex-int/nest-infra';

@Controller('api')
export class ApiController {
  @Post('create')
  @UseGuards(SecretkeyGuard)
  async create() {
    ...
  }
}
```

Контроллер:

```ts
import { Controller, Post, UseGuards } from '@nestjs/common';
import { SecretkeyGuard } from '@yandex-int/nest-infra';

@Controller('api')
@UseGuards(SecretkeyGuard)
export class ApiController {
  @Post('create')
  async create() {
    ...
  }
}
```

Глобально:

```ts
import { Module, APP_GUARD } from '@nestjs/common';
import { SecretkeyModule, SecretkeyGuard } from '@yandex-int/nest-infra';

@Module({
    imports: [SecretkeyModule.register(/* SecretkeyOptions */)],
    providers: [
        {
            provide: APP_GUARD,
            useClass: SecretkeyGuard,
        },
    ],
})
export class AppModule {}
```

При этом стоит помнить, что при использовании в контроллерах и методах необходимо в модуль контроллера / метода заимпортить `SecretkeyModule`

```ts
import { Module } from '@nestjs/common';
import { SecretkeyModule } from '@yandex-int/nest-infra';

// Если хотите использовать дефолтные настройки
@Module({
    imports: [SecretkeyModule],
})
export class ApiModule {}

// Если хотите выставить настройки
@Module({
    imports: [SecretkeyModule.register(/* SecretkeyOptions */)],
})
export class ApiModule {}
```

Можно подключить глобально

```ts
import { Module } from '@nestjs/common';
import { SecretkeyModule } from '@yandex-int/nest-infra';

// Если хотите выставить настройки
@Module({
    imports: [SecretkeyModule.forRoot(/* SecretkeyOptions */)],
})
export class ApiModule {}
```

## SecretkeyOptions

````ts
type SecretkeyOptions = {
    /**
     * HTTP методы, которые будут игнорироваться при проверке secretkey
     *
     * Default: ['GET', 'HEAD', 'OPTIONS']
     */
    ignoreMethods?: string[];

    /**
     * Функция, возвращающая secretkey из объекта req
     *
     * Default:
     * ```
     * req => (req.body && req.body.sk) ||
     *     (req.query && req.query.sk) ||
     *     req.headers['csrf-token'] ||
     *     req.headers['xsrf-token'] ||
     *     req.headers['x-csrf-token'] ||
     *     req.headers['x-xsrf-token'];
     * ```
     */
    value?: (req: Request) => string;

    /**
     * Версия secretkey. Может иметь значение 1 или 2
     *
     * Default: 1
     */
    version?: number;

    /**
     * Соль. Обязательна при использовании версии 2
     *
     * Default: ''
     */
    salt?: string;
};
````
