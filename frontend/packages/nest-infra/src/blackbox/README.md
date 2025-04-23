# blackbox

Nest обертка над `@yandex-int/express-blackbox`

Экспортирует:

```ts
export {
    BlackboxModule, // Модуль
    BlackboxService, // Сервис
    BlackboxOptions, // Тайпинги конфига
    Blackbox, // Тайпинги blackbox данных
};
```

## BlackboxModule

Экспортирует сервис `BlackboxService`

Подключается в `appModule` единожды
Для работы необходим `AsyncStorageModule` и `TvmModule`

```ts
import { Module } from '@nestjs/common';
import { AsyncStorageModule } from '@yandex-int/nest-common';
import { BlackboxModule, TvmModule } from '@yandex-int/nest-infra';

@Module({
    imports: [
        BlackboxModule.forRoot(/* BlackboxOptions */),
        /*
          либо через forRootAsync, если необходимо инжектить конфиг
          BlackboxModule.forRootAsync({
            imports: [ConfigModule],
            inject: [ConfigService],
            useFactory: (configService: ConfigService) => configService.config.blackbox, // BlackboxOptions
          })
        */
        AsyncStorageModule.forRoot(),
        TvmModule.forRoot(),
    ],
})
export class AppModule {}
```

## BlackboxService

Может запросить blackbox данные `.getBlackbox()`

```ts
import { BlackboxService } from '@yandex-int/nest-infra';

export class SomeService {
  constructor(private blackboxService: BlackboxService) {}

  async method () => {
    const blackbox = await this.blackboxService.getBlackbox();
  }
}
```

## BlackboxOptions

```ts
// Взято из express-blackbox
type BlackboxOptions = {
    /**
     * Email, which is checked on an accessory to the user.
     *
     * Required if value of emails options is "testone"
     */
    addrtotest?: string;

    /**
     * Get user login aliases
     *
     * Could be list of numbers separated by commas from this table:
     * https://wiki.yandex-team.ru/passport/dbmoving/#tipyaliasov
     */
    aliases?: 'getsocial' | 'getphonenumber' | 'all' | string;

    /** Passport API host */
    api:
        | 'blackbox.yandex-team.ru'
        | 'blackbox.yandex.net'
        | 'blackbox-mimino.yandex.net'
        | 'blackbox-test.yandex.net'
        | string;

    /**
     * Request user attributes into map
     *
     * Full list:
     * https://wiki.yandex-team.ru/passport/dbmoving#tipyatributov.
     *
     * By default:
     * {
     *   login: '1008',
     *   fio: '1007',
     *   sex: '29',
     *   email: '14',
     *   country: '31',
     *   lang: '34',
     *   avatar: '98'
     * }
     */
    attributes?: ExpressBlackbox.AttributesMap;

    /** Phone attributes
     * https://doc.yandex-team.ru/blackbox/reference/MethodUserInfo.html#format__phone_attributes
     */
    phones?: {
        kind: 'all' | 'bound';
        attributes: Record<string, ExpressBlackbox.PhoneAttributeKind>;
    };

    /**
     * Get additional authorization info,
     * authorization cookie creation date for example
     */
    authid?: 'yes';

    /** Get user emails */
    emails?: 'getall' | 'getyandex' | 'getdefault' | 'testone';

    /** Request format (JSON or XML)  */
    format?: 'json' | 'xml';

    /** Get user real addresses */
    getlocation?: 'postal';

    /** Get user info even if cookie was expired or account was blocked  */
    full_info?: 'yes'; // eslint-disable-line camelcase

    getServiceTicket?: (req: Request, res: Response) => Promise<string> | string | undefined;

    /** Oauth token, if true it will be extracted from Authorization header */
    oauth?: string | boolean;

    /** Get all accounts from cookie (incompatible with OAuth) */
    multisession?: 'yes';

    /** Number of request addtional attempts */
    retries?: number;

    /** Request timeout */
    timeout?: number;

    /** Get any custom yabox options which will be override and extend generic options  */
    getYaboxOptions?: (req: Request, res: Response) => object;
};
```
