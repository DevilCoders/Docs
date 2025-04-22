# HTTP server

HTTP сервер, являющийся оберткой над express и инкапсулирующий логику web сервиса, а именно:

-   Аутентификацию
-   Роутинг
-   Логирование/протоколирование запросов
-   Возможность отключить логирование для каждого хендлера
-   Профилирование времени обработки запроса
-   Разметка запросов reqId
-   Ping handler и graceful shutdown
-   Конфигурацию стандартных express middleware
-   Обработку ошибок
-   Назначение контректных хендлеров (ручек) через декораторы
-   Обработка multipart form data

**Мотивация: отделить бизнес логику от общих нюансов работы web сервера**

Контроллер это класс, содержащий набор методов, являющихся обработчиками http запросов (хендлерами) Контроллеры и
хендлеры, размещаются с помощью декораторов:

-   Controller // декоратор контроллера
-   GET // обработчик GET запроса
-   POST // обработчик POST запроса
-   PUT // обработчик PUT запроса
-   DELETE // обработчик DELETE запроса

#### Пример контроллера:

GET /example/my-handler POST /example/post-handler с отключенным логированием

```
@RestController('example')
export class ExampleController  {
    @Get('my-handler')
    public getHandler(req: Request, ctx: RequestContext) {
        return 'OK';
    }

    @Post({ path: 'post-handler', isLoggingDisabled: true })
    public postHandler(req: Request, ctx: RequestContext) {
        return { result: 'OK' }
    }
}
```

#### Как отдать файл?

При необходимости отдать в ответе файл следует вернуть из обработчика объект класса `File`. У файла можно задать
содержимое и **Content-Type**.

```
@RestController('example')
export class ExampleController  {
    @Get('my-document')
    public getDocument(req: Request, ctx: RequestContext) {
        const fileBlob = getDocument();
        return new File(
            'application/pdf',
            fileBlob
        );
    }
}
```

#### Request flow

1. Ping handler -> END
2. JSON body parser -> GOTO 3
3. (OPTIONAL) cookie parser -> GOTO 4
4. Init request id, timer and logger -> GOTO 5
5. (OPTIONAL) Authentication -> GOTO 6 | 8
6. (OPTIONAL) Init request context (authorization or other context) -> GOTO 7 | 8
7. App Router -> GOTO 8 | 9 | END
8. Error Handler -> END
9. Not Found Handler -> END

#### Http Code Mapping

Для того, чтобы вернуть status_code !== 200, необходимо бросить исключение с RuntimeError

Маппинг RuntimeError type:

-   400 - BAD_REQUEST_ERROR
-   401 - UNAUTHORIZED_ERROR
-   403 – FORBIDDEN_ERROR
-   404 – NOT_FOUND_ERROR

Любое другое исключение вернет 500 код

#### Authentication

Из коробки поддерживаются след виды аутентификации:

-   Disabled – дефолтная аутентификация отключена, можно делать кастомную в функции формировании контекста.
-   Basic – basic аутентицикация. Извлекает credentials из содержимого Authorization заголовка, декодирует и складывает
    в credentials
-   TvmService – tvm аутентикация сервиса. Поддерживает X-Ya-Service-Ticket. Как итог – tmvSeviceId в объекте Request.
-   TvmUser – tvm аутентикация uid Яндекса от стороннего сервиса. Поддерживает X-Ya-Service-Ticket и X-Ya-User-Ticket.
    Как итог – tmvSeviceId и tvmUids в объекте Request.
-   Blackbox - аутентицикация пользователя Яндекс в сервисе blackbox. Информация об аутентифицированном пользователе
    хранится в поле `userInfo` объекта Request. Для использования Blackbox-аутентификации необходимо:
    -   Подкючить cookie parser (флаг `isCookieParserEnabled`),
    -   Настроить в TVM-демоне получение тикетов к Blackbox с alias `'blackbox'`.

В случае неуспешной аутентификации отправляется UNATHORIZED

#### RequestContext and Handlers

В RestServer можно передать ContextProvider, который будет формировать контекст для каждого запроса. Наиболее частое его
применение, это получение авторизационных данных.

Ожидается, что handler запроса будет соответствовать след сигнатурам:

1. Если ContextProvider был передан в опциях:
    ```typescript
    type RequestHandler<TContext> = (req: Request, ctx: TContext) => Promise<any>;
    ```
    где TContext это тип контекса, фомируемый ContextProvider (например, авторизация)
2. Если ContextProvider отсутствует:
    ```typescript
    type RequestHandler = (req: Request) => Promise<any>;
    ```

#### Logger

-   В методе формирования контекста при добавлении тегов не стоит форкать request.logger, переключая контекст.
-   Для сохранения тэгов в контексте вывода логов следует использовать request.logger (можно форкать)
-   С помощью флага isLoggingDisabled можно отключить логирование конкретного хендлера

#### Content-Security-Policy

Логику генерации хедера нужно реализовывать в месте использования сервера. Сделать это можно через
`responseHeadersProvider` в параметрах `ControllersGroup`. Есть класс `CspBuilder`, который реализует логику
формирования значения для хедера:

-   Если есть инлайновые скрипты, то нужно использовать `nonce` для их подписи, хелпер для генерации есть в
    `csp/nonce.ts`.

    -   getCspHeader.ts
        ```typescript
        import { CspBuilder } from '@server-libs/http-server/csp/builder';
        import { CspDirective, CspDirectiveValue } from '@server-libs/http-server/csp/types';
        ...
        const cspString = new CspBuilder()
            .setDirectives({
                [CspDirective.ScriptSrc]: [CspDirectiveValue.Nonce],
            })
            .build(nonceId);
        ...
        ```
    -   index.html
        ```html
        ...
        <script nonce="nonceId">
            console.log('inline script');
        </script>
        ...
        ```

-   Генерирует `report-uri` для отправки отчётов нарушения политик в сервис https://csp.yandex-team.ru, подробнее в
    [этушке](https://clubs.at.yandex-team.ru/security/13881)
