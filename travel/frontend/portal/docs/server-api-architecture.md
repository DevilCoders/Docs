# Архитектура API BFF

> BFF - Backend For Frontend приложения путешествий, написанный на nodejs

API BFF состоит из нескольких слоёв:

1. HTTP Client
2. API Client
3. Service
4. Controller

## HTTP Client

**HTTP Client** — модуль, который отвечает за отправку запросов в эндпоинты других API. Этот модуль должен предоставлять возможность отправлять Get/Post/Put/Delete и прочие запросы.

Также включает в себя проброс и установку идентификатора запроса, который может храниться в каком-либо хедере. Идентификатор запроса должен всегда логироваться и позволять по логам отследить цепочку запросов в одном контексте. Приведём пример:

В BFF прилетает запрос получить записную книжку пользователя. Определяется контекст этого запроса. В express им является `req` во всех миддлварях

Для этого запроса нужно выполнить четыре запроса в API записной книжки:

-   получить контакты пользователя
-   получить всех пассажиров пользователя
-   получить все документы всех пассажиров
-   получить все бонусные карты всех пассажиров

При отправке запроса http-клиент проверяет наличие идентификатора запроса в контексте запроса. Если его нет то генерирует uid и кладёт его в контекст. Затем проставляет этот идентификатор в хедер (TODO: определить хедер) при отправке запроса в API записной книжки.

Каждый запрос должен быть залогирован, желательно сохранить в логе статус ответа, время выполнения запроса,метод и полный адрес запроса. В зависимости от статуса ответа и нагрузки на сервис можно проставлять нужный уровень логирования (возможно не очень интересно писать в логи успешные запросы). В дев-режиме удобно выводить body запроса и body ответа. Но только в дев-режиме.

Таким образом если один из 4 запросов в данном контексте упадёт, легко по логам можно будет восстановить всю историю.

**TODO: решить что у нас будет HTTP Client**. Например, это может быть надстройка над `axios`

Перейдём дальше, к **API Client**

## API Client

**API Client** — модуль, обёртка над **HTTP Client**.
Этот модуль знает как отправлять в указанную API. Должен предоставлять удобный интерфейс обращения к API, в виде вызова метода. Позволяет вместо

```js
const passengers = await httpClient.get(`${travelersApiEndpoint}/passengers`, {
    params: {id},
    headers,
});
```

писать

```js
const passengers = await travelersApi.getPassengers(id);
```

Лучше всего такой модуль инициализировать на каждый запрос, если он зависит от контекста запроса, например от авторизации пользователя.

В общем случае это класс унаследованный от базового класса для клиентов к API:

```ts
class TravellersApi extends RestApiClient {
    protected logger: ILogger;

    protected baseURL: string;

    private userTicket: UserTicket;

    public contructor({logger, baseURL, userTicket}: TravellersApiConfig) {
        this.logger = logger;
        this.baseURL = baseURL;
        this.userTicket = userTicket;
    }

    public getPassengers(id: string): TravelerPassengerDTO[] {
        return this.get<TravelerPassengerDTO[]>('/passengers', {id});
    }

    protected async interceptRequest(request: IRequestOptions) {
        const serviceTicket = await getServiceTicket(
            config.tvm.frontend.id,
            config.tvm.frontend.client,
            config.tvm.travelers.id,
        );
        request.headers = {
            'X-Ya-Service-Ticket': serviceTicket,
            'X-Ya-User-Ticket': this.userTicket,
        };
    }
}
```

Таким образом вся логика обращения к API записной книжки будет скрыта внтури клиента `TravellersApi`. Это добавляет читабельности коду, а также улучшает его переиспользование.

Все данные которые приходят от других API, а также те что к ним отправляются, помечаются суффуксом **DTO**.

> DTO - data transfer object

DTO является простым объектом без каких либо методов или приватных свойств, и состоит только из примитивных типов, например для даты используются строки (это нужно для однозначной сериализации объекта в JSON). Общение с другими сервисами всегда должно происходить через DTO.

Стоит отметить, что API клиент может возвращать инстанс класса, полученный путём преобразования DTO к этому инстансу класса. Это может быть полезно если часто приходится преобразовывать DTO в какой-нибудь внутренний класс.

Клиенты к API позволяют только получать и отправлять данные. Но специфика приложения привносит, то что нужно эти DTO преобразовывать, изменять, объеденять для того, чтобы передать их в удобном формате на клиент. А также объеденять ответы от разных API и выполнять различную специфичную для бизнеса логику. Всё это происходит в сервисах

## Service

Service — модуль, который оперирует всей бизнес логикой. Обычно это класс (или функция-фабрика), который в конструкторе принимает все зависимости в виде клиентов к апи, логгера и прочего, что может понадобиться сервису.

Пример сервиса записной книжки

```ts
class TravelersServive {
    private travelersClient: ITravelersClient;

    public constructor(travelersClient: ITravelersClient) {
        this.travelersClient = travelersClient;
    }

    public async saveDocuments(documents: FormDocumentDTO[]) {
        // some logic with documents and travelersClient
    }
}
```

Такая структура позволяет легко подменять зависимость сервиса от клиента к апи, что удобно для тестирования бизнес-логики

## Controller

Controller — модуль, который занимается обработкой запроса, извленчения из него данных и передачи их сервису. Также в его ответственность включается обработка ошибок. **Controller** не должен содержать в себе никакой бизнес логики и должен быть максимально простым.

По аналогии с сервисами, контроллеры обычно создаются в виде классов или фабрик, принимающих в параметры инициилизации зависимости в виде сервисов.

```ts
class TravelersController {
    private travelersService: ITravelersService;

    public constructor(travelersService: ITravelersService) {
        this.travelersService = travelersService;
    }

    @bodyParser('json')
    public async saveDocumentsFromForm(req: Request, res: Response) {
        const body: DocumentsFormDTO = req.body;
        try {
            await this.travelersService.saveDocuments(body.documents);
            res.send();
        } catch (ex) {
            if (ex.response) {
                res.status(ex.response.status).send(ex.response.body);
            } else {
                res.status(502).send();
            }
        }
    }
}
```

## Обработка ошибок

**TODO:** единный формат ошибок и один верхнеуровневый хендлер ошибок

## Инициилизация зависимосте в классах и фабриках

**TODO**: пример работы с DI контейнером на примере [awilix](https://github.com/jeffijoe/awilix)
