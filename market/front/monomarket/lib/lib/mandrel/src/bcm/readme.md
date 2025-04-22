Что требуется чтобы всё заработало
==============================

- В конфигах проекта для окружения development (ака configs/development/node.js) добавляем секцию:

```json
{
  "tvm": {
    "env": "market_front_desktop"
  }
}
```

- конфигах проекта для окружения тестинг и продакшн добавляем секцию:

```json
{
  "tvm": {
    "env": "market_front_desktop",
    "configPath": "../../tvm-daemon/tvmtool.conf",
    "authPath": "../../tvm-daemon/local.auth"
  }
}
```

Проверяем что в файлах `tvm.json` указаны все бекенды в которые будет ходить приложение, используя TVM.

Для logrus'ов этот конфиг общий и хранится в `/etc/tvmtool/tvmtool.conf`, изменения в него желательно не вносить вручную - это делается централизованно через репозиторий `provision`

Список бекендов которые обязательно должны быть указаны в `tvm.json`:
  - blackbox (см https://wiki.yandex-team.ru/passport/tvm2/user-ticket/#0-opredeljaemsjasokruzhenijami)
  - social (см https://abc.yandex-team.ru/resources/?search=social%20api&supplier=14&type=47&state=requested&state=approved&state=granted)

Названия бекендов в `tmv.json` совпадают с названиями в основном конфиге в секции `servant` - стоит перепроверить, что в `servant` конфиге правильно указаны хосты, в каждом окружении.

Как писать бекенды
================

Если в бекенде не требуется использование TVM, используем в качестве базового бекенда `MarketBackend`:

```typescript
import {MarketHttpBackend} from '@yandex-market/mandrel/bcm/base';
```

Если требуется использование TVM, но не требуется авторизация, то используем `AbstractTVMBackend`:
```typescript
import {AbstractTVMBackend} from '@yandex-market/mandrel/bcm/abstract';
```

Если требуется использовать TVM и авторизацию, то используем `AbstractTVMAuthBackend`:
```typescript
import {AbstractTVMAuthBackend} from '@yandex-market/mandrel/bcm/abstract';
```

Далее декларируем наш бекенд:
```typescript
import {HttpTransportResponseError, HttpTransportResponse} from '@yandex-market/mandrel/bcm';
import {MarketHttpTransportParams} from '@yandex-market/mandrel/bcm/base';
import {AbstractTVMAuthBackend} from '@yandex-market/mandrel/bcm/abstract';

export class SomeBackend extends AbstractTVMAuthBackend.setup('backendNameInServantConfig', {
    // конфиг по-умолчанию. переопределяется позже конфигом из servant

    internal: false, // если true - никогда не ходим в кадавр

    pathname: '/base/path',
    query: {base: 'query-params'},
    headers: {globalHeader: 'value'},
    proxyHeaders: ['some-header-to-proxy-thru'],
    encodeBody: 'json',
    traceId: 'trace-log-backend-name',
    agent: {name: 'agent-name', maxSockets: 500},

    /**
     * При запросах описывает как массивы преобразуются в строку параметров.
     * Значения: 'bracket' | 'index' | 'comma' | 'none' | 'default'. Дефолтное: 'default'.
     * Пример: https://github.com/sindresorhus/query-string#arrayformat-1
     * 'default' - для обратной совместимости. Массив преобразуется в строку с запятыми:
     * {a: [1,2,3]} => "?a=1%2C2%2C3"
     */
    queryArrayFormat: QueryArrayFormat,
    /**
     * Указывает что при запросах надо оставлять ключи в query если они null.
     * Значение: boolean. Дефолтное: false.
     * true: {a: null, b: 1, c: undefined} => "?a&b=1"
     * false: {a: null, b: 1, c: undefined} => "?b=1"
     */
    queryKeepNull: boolean,
    /**
     * Указывает, надо ли трактовать параметр query, как строку, или оставить нетронутой строкой
     * @default false
     */
    queryString: boolean,

    autotestModifier(params) {
        params.headers.autoTest = '1';
        return params;
    },

    expModifier(params, expFlags, fapiRearrFactors) {
        if (expFlags['exp_flag']) {
            params.host = 'exp-host';
        }

        return params;
    },

    followRedirect: false,
    decompress: true,
    encoding: 'utf8',
    parseBody: 'json',
    timeout: 1000,
    retry: 3,
    retryDelay: 100,
    retryAllowed: error => error instanceof HttpTransportResponseError && error.statusCode >= 500,
    acceptStatusCode: statusCode => [200, 201].includes(statusCode),
}) {
    // при необходимости переопределяем метод prepareRequest
    public async prepareRequest(
        params: MarketHttpTransportParams
    ): Promise<MarketHttpTransportParams> {
        const prepared = await super.prepareRequest(params);
        prepared.query.prepared = 1;
        return prepared;
    }

    // при необходимости переопределяем метод prepareResponse
    public async prepareResponse(
        response: HttpTransportResponse,
        params: MarketHttpTransportParams
    ): Promise<any> {
        const prepared = await super.prepareResponse(response, params);
        return prepared.some.field;
    }
}
```

Как писать клиенты
================

Описываем в какой бекенд будет ходить клиент и какие методы будут реализованы.

```typescript
import {MarketClient} from '@yandex-market/mandrel/bcm/base';

export class SomeClient extends MarketClient.connect({
    backend: SomeBackend, // Указываем бекенд в который будет ходить клиент
}) {
    public async someMethod(param1, param2): Promise<{value: string}> {
        const result: {value: boolean} = await this.backend.fetch({
            logName: "someMethod", // обязательный параметр - название метода для лога
            // остальные параметры необязательны
            method: "POST",
            pathname: "/path/to/backend/endpoint/",
            query: {someParams: param1},
            headers: {'some-header-in-css-case-lowercase': param2},
            body: {some: {content: 'in body'}},
            timeout: 123, // опциональный параметр. позволяет переопределять таймаут заданный для бекенда
            fullResponse: false, // если true - возвращет не body, а целиком ответ (body, headers, statusCode, statusMessage)
            proxyHeaders: ['some-header-to-proxy-thru']
        });

        return {value: result.value ? 'success' : 'failure'};
    }
}
```

Как использовать клиенты
=====================

Для того чтобы получить инстанс нужного класса, нужно его создать с помощью фабрики и контекста:

```typescript
const client = SomeClient.factory(ctx);
client === SomeClient.factory(ctx); // на один контекст создаётся один инстанс
```

Ну а далее просто вызываем нужные методы с теми аргументами которые описаны.

```typescript
SomeClient.factory(ctx).someMethod('asdf', 'qwerty').then(
    (result) => console.log('success', result),
    (error) => console.log('error', error)
);
```
