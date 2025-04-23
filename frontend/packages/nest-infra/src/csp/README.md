# csp

Nest обертка над `@yandex-int/express-yandex-csp`

Экспортирует:

```ts
export {
  CspModule, // Модуль
  CspService, // Сервис
  CspInterceptor, // Интерсептор
  CspOptions, // Тайпинг настроек
  // Так же константы для правил:
  CSP: {
    EVAL,
    INLINE,
    NONE,
    SELF,
    NONCE,
    TLD,
  },
};
```

## CspModule

Модуль экспортирует сервис `CspService` и интерсептор `CspInterceptor`
Для работы необходим `AsyncStorageModule`

```ts
import { Module } from '@nestjs/common';
import { AsyncStorageModule } from '@yandex-int/nest-common';
import { CspModule } from '@yandex-int/nest-infra';

@Module({
    imports: [
        CspModule.register(/* CspOptions */),
        // или если использовать дефолтные настройки
        // BlackboxModule
        AsyncStorageModule.forRoot(),
    ],
})
export class AppModule {}
```

## CspService

Имеет 2 метода: `.getCspData()` - возвращает объект

```ts
{
    header: string; // заголовок, в который необходимо поместить csp строку
    cspString: string; // строка с csp правилами
    nonce: string | null; // сгенерированный nonce
}
```

И `.getNonce()` - возвращает только nonce из предыдущего метода

## CspInterceptor

Генерирует и подсобывает в зогловки csp правила

Может подключается как и любой интерсептор в 3 места

Метод:

```ts
import { Controller, Post, UseInterceptors } from '@nestjs/common';
import { CspInterceptor } from '@yandex-int/nest-infra';

@Controller('api')
export class ApiController {
  @Post('create')
  @UseInterceptors(CspInterceptor)
  async create() {
    ...
  }
}
```

Контроллер:

```ts
import { Controller, Post, UseInterceptors } from '@nestjs/common';
import { CspInterceptor } from '@yandex-int/nest-infra';

@Controller('api')
@UseInterceptors(CspInterceptor)
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
import { CspModule, CspInterceptor } from '@yandex-int/nest-infra';

@Module({
    imports: [
        CspModule.register(/* CspOptions */),
        // или если использовать настройки по-умолчанию
        // CspModule,
    ],
    providers: [
        {
            provide: APP_INTERCEPTOR,
            useClass: CspInterceptor,
        },
    ],
})
export class AppModule {}
```

При этом стоит помнить, что при использовании в контроллерах и методах необходимо в модуль контроллера / метода заимпортить `CspModule`

```ts
import { Module } from '@nestjs/common';
import { CspModule } from '@yandex-int/nest-infra';

// Если хотите использовать дефолтные настройки
@Module({
    imports: [CspModule],
})
export class ApiModule {}

// Если хотите выставить настройки
@Module({
    imports: [CspModule.register(/* CspOptions */)],
})
export class ApiModule {}
```

Можно подключить `CspModule` глобально:

```ts
import { Module } from '@nestjs/common';
import { CspModule } from '@yandex-int/nest-infra';

// Если хотите выставить настройки
@Module({
    imports: [CspModule.forRoot(/* CspOptions */)],
})
export class ApiModule {}
```

## CspOptions

```ts
type CspOptions = {
    /**
     * Объект вида "ключ => массив строк" с политиками CSP. Если не указан исполльзуются дефолтные правила
     */
    policies?: Policies;
    /**
     * Пресеты правил. https://github.yandex-team.ru/toolbox/express-yandex-csp#Пресеты-список
     */
    presets?: Array<Policies | string> | Record<string, Policies | string>;
    /**
     * Адрес для отсылки отчетов о нарушении политики
     */
    reportUri?: string | Function;
    /**
     * Флаг использования адреса для отчетов, рекомендованного отделом ИБ.
     * При установке в true отменяет предыдущий параметр.
     */
    useDefaultReportUri?: boolean;
    /**
     * Название (идентификатор) вашего сервиса (отправляется в поле from). Обязателен при useDefaultReportUri: true.
     */
    serviceName?: string;
    /**
     * Название (идентификатор) вашего сервиса (отправляется в поле project).
     * Если не передано, то используется serviceName.
     */
    project?: string;
    /**
     * Опции парсинга TLD для автоматической подстановкив правила
     */
    domainOptions?: {
        customTlds: RegExp | Array<string>;
        privateTlds?: boolean;
    };
};
```
