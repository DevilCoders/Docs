# Подход к построению архитектуры клиентских запросов и использованию BrowserHttpClient

> BrowserHttpClient - браузерный модуль, который отвечает за отправку запросов с клиента на сервер.

## Структура клиентских запросов

Для инициации запроса, например в redux(saga или thunk), необходимо использовать соотвествующий метод определенного serviceProvider.

> serviceProvider - изоморфный модуль, который позволяет получать ресурсы и для SSR и для Browser.

Все модули подобного типа находятся в директории `src/serviceProvider/$PROJECT/$SERVICE_NAME/...`.
В зависимости от того, на какой стороне выполняется код данного serviceProvider(server или browser), используются различные модули:

-   server: `server/services/$SERVICE_NAME`;
-   browser: `src/serviceProvider/$PROJECT/$BROWSER_PROVIDER_NAME`;

> browserProvider - браузерный модуль, который наследуется от BrowserHttpClient, описывает все запросы к серверу данного "Service" и имлементирует интерфейс соотвествующего "Service" на сервере.

## Примеры работы с browserProvider на основе BrowserHttpClient

_BrowserHttpClient_ предоставляет набор методов базового **HttpClient** ("get", "post", "put", "delete", "patch").
Каждый _browserProvider_ отвечает за определенный набор ресурсов, которые можно получить с его помощью используя методы _BrowserHttpClient_.

Пример построения **browserSearchHotelsProvider** для получения списка отелей в рамках Service поиска отелей:

```ts
import {BrowserHttpClient} from 'utilities/browserHttpClient/BrowserHttpClient';
import {IHotelsSearchService} from 'server/services/HotelsServices/HotelsSearchService';
import {
    ISearchPollingParams,
    ISearchHotels,
} from 'server/api/HotelsSearchAPI/types/ISearchHotels';

export class BrowserSearchHotelsProvider
    extends BrowserHttpClient
    implements IHotelsSearchService
{
    public constructor() {
        super({baseURL: HOTELS_BASE_API});
    }

    public searchHotels = (
        searchPollingParams: ISearchPollingParams,
    ): Promise<ISearchHotels> => {
        return this.get<ISearchHotels>(SEARCH_HOTELS_POLLING, {
            params: searchPollingParams,
        });
    };
}

export const browserSearchHotelsProvider = new BrowserSearchHotelsProvider();
```

**BrowserHttpClient** отвечает за простановку базовых заголовков("x-csrf-token", "Pragma"). Если нужны кастомные заголовки или параметры запроса, то можно определить метод _interceptRequest_ и поправить необходимые параметры.  
Параметр _baseURL_ указывает базовый путь до вашего api backend. Также можно указать кастомный конфиг _httpClientConfig_ (AxiosRequestConfig) и _timeout_ для **HttpClient**.

Пример добавления кастомного заголовка:

```ts
    // Вариант с одним заголовком
    protected async interceptRequest(request: IRequestOptions) {
        request.headers['X-Ya-My-Custom-Header'] = myCustomHeaderValue;
    }

    // Вариант с несколькими заголовками
    protected async interceptRequest(request: IRequestOptions) {
        request.headers = {
            ...request.headers,
            'X-Ya-My-Custom-Header': myCustomHeaderValue,
            'X-Ya-My-Custom-Header-2': myCustomHeaderValue2,
        };
    }
```

## Рекомендации по описанию параметров и получаемых ресурсов.

-   Достаточно удобно описывать все параметры запросов уже на стороне "Server" и импортить для **browserProvider**.
    Тем самым у нас всегда синхронизованно то, что мы отсылаем с клиента и получаем на сервере. В примере выше это _ISearchPollingParams_.
-   Также удобно описывать типы и подготавливать получаемые ресурсы на стороне "Server" и использовать их потом на клиентской стороне. В примере выше это _ISearchHotels_.
