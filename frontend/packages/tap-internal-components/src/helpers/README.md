# helpers

## experiments

Используется для работы с флагами экспериментов.
```ts
type FlagMap = Record<string, FlagValue>;
type FlagValue = string | number | boolean;
type BooleanParser = (arg?: unknown) => boolean;
type NumberParser = (arg?: unknown) => number;
type StringParser = (arg?: unknown) => string;
type FlagParser = BooleanParser | NumberParser | StringParser;
type FlagParserMap = Record<string, FlagParser>;

// Документация https://wiki.yandex-team.ru/users/buryakov/Format-vydachi-kommunalnogo-servisa-flagov/
type ExperimentsConfig = {
  exphandler: string; // имя хендлера. id отдельной комнаты в коммуналке, так сказать.
  flags_json_version: string; // использованная версия flags.json (сквозная нумерация по всем сервисам)
  exp_config_version: string; // использованная версия конфига экспериментов
  exp_boxes: string; // выборки - ответ Разбивалки aka UaaS
  exp_boxes_crypted: string; // зашифрованные выборки (для записи в Метрику) - ответ Разбивалки aka UaaS

  // сработавшие выборки из ответа Разбивалки
  // (могут быть не все, т.к. в выборке может быть condition, который не сработал)
  ids: string[];

  is_prestable: 0; // зарезервировано; на данный момент - 0
  all: {
    // здесь содержатся смёрженные флаги
    CONTEXT: {
      MAIN: Record<string, FlagMap>; // глобальная настройка для текущего запроса
    } & {
      [key: string]: FlagMap;
    };

    // список выборок из flags.json (выкаченные на 100%) + сработавшие выборки от Разбивалки (эксперименты)
    TESTID: string[];
  } & {
    [key: string]: FlagValue; // флаги заданные через cgi-параметр exp_flags; пример: exp_flags=cgiFlag=1
  };

  // зашифрованное состояние бекенда; подробности есть в основной документации
  // https://wiki.yandex-team.ru/users/buryakov/Kommunalnyjj-servis-dlja-flags.json/#versiontoken
  version_token: string;

  // request id запроса, пример: "1593013530381167-1013613128265517090900130-vla1-1997-vla-shared-app-host-8423"
  reqid: string;
};

type ResponseError = {
  error: {
    name: string;
    message: string;
    data?: object;
  }
};

type FetchConfigSuccessCallback = (config: ExperimentsConfig) => void;
type FetchConfigErrorCallback = (error: ResponseError['error']) => void;
```

### ExperimentsContext & ExperimentsProvider

Компонент-провайдер флагов экспериментов. Для получения флагов экспериментов вызываем `flagsFetcher`, ждём
`timeout` времени, если запрос не успел завершиться за это время, берём флаги из кэша по ключу `storageKey`,
но в фоне дожидаемся загрузки актуальных флагов.

Свойства:
```ts
type DataProviderOptions = {
  storageKey: string; // ключ, по которому будем хранить флаги в localStorage
  timeout?: number; // таймаут, по которому берём флаги из кэша
};

type ExperimentsHandlerOptions<T extends FlagParserMap> = DataProviderOptions & {
  handler: string;
  flagParsers: T, // парсеры флагов
  onFetchConfigSuccess?: FetchConfigSuccessCallback;
  onFetchConfigFailed?: FetchConfigErrorCallback;
  flagsFetcher?: () => Promise<FlagMap>; // запрос за флагами
};

type ExperimentsProviderProps<T extends FlagParserMap> = ExperimentsHandlerOptions<T> & {
    children?: ReactNode
};
```

### useExperimentValue

Используется для получения значения конкретного флага экспериментов.
```ts
function useExperimentValue<T extends FlagParserMap, K extends keyof T>(flagParsers: T, key: K): ReturnType<T[K]> | undefined | null;
```

### useIsExperimentsLoaded

Используется для определения статуса загрузки флагов экспериментов.

```ts
function useIsExperimentsLoaded(): boolean;
```

## request
```ts
type Endpoint = string;
type Options = Omit<RequestInit, 'headers' | 'method'> & {
    headers?: Record<string, string>;
    method?: HttpMethod;
};
enum HttpMethod {
    CONNECT = 'CONNECT',
    DELETE = 'DELETE',
    GET = 'GET',
    HEAD = 'HEAD',
    OPTIONS = 'OPTIONS',
    PATCH = 'PATCH',
    POST = 'POST',
    PUT = 'PUT',
    TRACE = 'TRACE',
}
type Request<R = Response, O = Options, M = {}> = (
    endpoint: Endpoint,
    options?: O,
    middlewareOptions?: M
) => Promise<R>;
type RequestOptions<R = RequestMiddleware> = { middleware?: Array<R> };
type RequestMiddleware<R extends Request<any, any, any> = any, RR extends Request<any, any, any> = any> = (
    request: R
) => RR;
```

### assertResponse

Используется в мидлварах для проверки типа результата предыдущей мидлвары.
```ts
function assertResponse(value: unknown, name: string): asserts value is Response;
```

### createRequest

Используется для создания функции запроса с определённым набором мидлвар.
```ts
function createRequest<O = Options, M = {}>(requestOptions: RequestOptions = {}): <R = Response>(endpoint: Endpoint, options?: O | undefined, middlewareOptions?: M | undefined) => Promise<R>;
```

Существующие мидлвары:
 * [cookie](###cookie)
 * [csrf](###csrf)
 * [network](###network)
 * [retry](###retry)

### cookie

Используется для обновления паспортных кук.

```ts
type CookieResponse = {
    status: string;
};

type CookieMiddlewareOptions = {
    cookiePassportHost?: string;
    cookieUpdateOnInit?: boolean;
};

function cookieMiddleware(defaultOptions?: CookieMiddlewareOptions): RequestMiddleware<Request, Request<Response, Options, CookieMiddlewareOptions>>;
```

### csrf

Используется для получения и обновления csrf-токенов в запросах.

```ts
type CachedToken = {
  token: string;
  validUntil: number;
};

type CsrfTokenResponse = {
  value: string;
  ttl: number;
};

type CsrfOptions = {
  apiUrl: string; // урл запроса за csrf-токеном
  headerName?: string; // заголовок, из которого будем получать токен. По-умолчанию X-Csrf-Token'
  localStorageKey?: string; // ключ для кэширования в localStorage. По-умолчанию csrf_token
  method?: HttpMethod.GET | HttpMethod.POST;
  parseToken: (response: Response) => Promise<CsrfTokenResponse>;
  validateResponse: (response: Response) => Promise<boolean>; // проверяет, нужно ли обновить токен
};

type CsrfDefaultOptions = CsrfOptions & {
  middleware?: Array<RequestMiddleware>;
}

type CsrfMiddlewareOptions = Partial<CsrfOptions>;

function csrfMiddleware(defaultOptions: CsrfDefaultOptions): RequestMiddleware<Request, Request<Response, Options, CsrfMiddlewareOptions>>;
```

### network

Используется для определения наличия сети с помощью [isNetworkConnectionFailed](###isNetworkConnectionFailed).
В случае отстутствия сети будет выброшено исключение `NetworkError`.

```ts
type NetworkMiddlewareOptions = NetworkAvailableOptions;

function networkMiddleware(defaultOptions: NetworkMiddlewareOptions): RequestMiddleware<Request, Request<Response, Options, NetworkMiddlewareOptions>>;
```

### retry

Используется для ретрая запросов.
```ts
type RetryFuncOptions = {
  attempt: number;
  retryCount: number;
  error: Error | null;
  response: Response | null;
  method: HttpMethod;
  allowedMethods: Set<HttpMethod>;
};

type RetryDelayFunction = (options: RetryFuncOptions) => number;
type RetryOnFunction = (options: RetryFuncOptions) => boolean;

type RetryMiddlewareOptions = {
    allowedMethods?: Set<HttpMethod>;
    retryCount?: number; // кол-во ретраев
    retryDelay?: number | RetryDelayFunction; // задержка между ретраями
    retryOn?: RetryOnFunction; // определяет, нужно ли делать ретрай
};

function retryMiddleware(defaultOptions?: RetryMiddlewareOptions): RequestMiddleware<Request, Request<Response, Options, RetryMiddlewareOptions>>;
```

## add-to-nav-panel
### addToNavPanel

Используется для добавления приложения на главный экран с помощью js-api.

```ts
type AddToNavPanelOptions = {
    onConfirm?: () => void;
    onCancel?: () => void;
    onNotShown?: () => void;
    onError?: (error: JSApiError | AddToNavPanelError) => void;
}

function addToNavPanel(options: AddToNavPanelOptions): Promise<void>;
```

## applepay

```ts
type PaymentMethodData = {
    regionId: number;
    countryCode: string;
    serviceToken: string;
    merchantIdentifiers: string[];
    recipientTitle?: string; // Default: Yandex
    enforcedTrustBaseUrl?: string; // Точка для оверрайда урла бекэнда Траста. Default: https://pcidss.yandex.net/api/
};
```

### getApplePayAvailability

Используется для проверки возможности оплаты через ApplePay с помощью js-api.
```ts
function getApplePayAvailability(paymentMethodData: PaymentMethodData, onError?: (error: Error) => void): Promise<boolean>; 
```

### getApplePayPaymentMethodId

Используется для вызова оплаты через ApplePay с помощью js-api, возвращает `payment_method_id`.
Если оплата по каким-то причинам не произошла - вернется `null`.
```ts
type GetApplePayPaymentMethodIdParams = {
    paymentMethodData: PaymentMethodData;
    paymentDetailsInit: PaymentDetailsInit;
    onError?: (error: Error) => void;
}
function getApplePayPaymentMethodId(params: GetApplePayPaymentMethodIdParams): Promise<string | null>;
```

## assert
### assertNonNullable

Используется для проверки наличия аргумента. Если аргумент равен `null` или `undefined` пробрасывается исключение.

## cookie
### parseCookies

Используется для получения кук текущего домена в виде объекта.
```ts
function parseCookies(): Record<string, string | undefined>;
```

## portal-auth

```ts
enum PassportMode {
    Testing,
    Production,
}

type LoginParams = {
    mode: PassportMode;
    origin?: string;
    retpath?: string;
    userInfoRequest?: UserInfoRequest;
    onWindowBlocked?: (error: BlockedWindowError) => void;
};

type UserInfoRequest = (params: { mode: PassportMode }) => Promise<YandexPortalUserInfo | null>;
type GetUserInfoParams = { 
    mode: PassportMode;
    userInfoRequest?: UserInfoRequest;
};

type BindPhoneParams = {
    mode: PassportMode;
    origin?: string;
    retpath?: string;
    userInfoRequest?: UserInfoRequest;
    onWindowBlocked?: (error: BlockedWindowError) => void;
};

type LogoutParams = {
    mode: PassportMode;
};

type ChangeAccountParams = {
    mode: PassportMode;
    origin?: string;
    retpath?: string;
    userInfoRequest?: UserInfoRequest;
    onWindowBlocked?: (error: BlockedWindowError) => void;
};
```

### login

Используется для авторизации в любом браузере. Сначала используется авторизация через `js-api`,
если она недоступна, то происходит авторизация через паспорт в отдельной вкладке с получением
данных о пользователе с помощью функции, переданной в `userInfoRequest`,
по-умолчанию запрашиваем из ручки `tap-backend`. В случае, когда открытие новой вкладки заблокировано,
происходит редирект на страницу паспорта.
```ts
function login(params?: Partial<LoginParams>): Promise<YandexPortalUserInfo>;
```

### getUserInfo

Используется для получения информации о пользователе в любом браузере. Сначала используется `js-api`,
если оно недоступно, то запрашиваем данные о пользователе с помощью функции, переданной в `userInfoRequest`,
по-умолчанию запрашиваем из ручки `tap-backend`. В случае, когда пользователь не авторизован, возвращается `null`.
```ts
function getUserInfo(params?: Partial<GetUserInfoParams>): Promise<YandexPortalUserInfo | null>;
```

### bindPhone

Используется для привязки номера телефона к аккаунту в любом браузере. Сначала используется `js-api`,
если оно недоступно, то привязка номера телефона происходит в отдельной вкладке. В случае, когда открытие новой
вкладки заблокировано, происходит редирект на страницу паспорта.
```ts
function bindPhone(params?: Partial<BindPhoneParams>): Promise<void>;
```

### logout

Используется для выхода из всех аккаунтов в любом браузере. Сначала используется `js-api`, 
если оно недоступно, то происходит запрос в паспорт.
```ts
function logout(params?: Partial<LogoutParams>): Promise<void>;
```

### changeAccount

Используется для смены аккаунта в любом браузере. Сначала используются `logout`
(при этом разлогиниваем из всех аккаунтов) и `login` из js-api, если они недоступны, то происходит смена
аккаунта через паспорт в отдельной вкладке с получением данных о пользователе с помощью функции,
переданной в `userInfoRequest`, по-умолчанию запрашиваем из ручки `tap-backend`.
В случае, когда открытие новой вкладки заблокировано, происходит редирект на страницу паспорта.
```ts
function changeAccount(params?: Partial<ChangeAccountParams>): Promise<YandexPortalUserInfo | null>;
```

## passport

```ts
enum PassportMode {
    Testing,
    Production,
}
```

## payment
### bindCardByPaymentRequest

Вызывает нативное окно с возможностью изменить список банковских карт с помощью js-api (Payment SDK).
```ts
type BindCardByPaymentRequestParams = { serviceToken?: string; yaBindingVersion?: number; };
function bindCardByPaymentRequest(params?: BindCardByPaymentRequestParams): Promise<boolean>
```

### getCardLabel

Возвращает текстовый лейбл карты.
```ts
type Card = { name?: string; number?: string; };
export function getCardLabel(card: Card): string
```

## clipboard
### copyToClipboard

Копирует переданную строку в буфер обмена.
```ts
function copyToClipboard(text: string): void
```

## geolocation

```ts
enum PositionErrorCodes {
    PermissionDenied = 1,
    PositionUnavailable = 2,
    Timeout = 3,
}
```

### requestGeolocationPermissions

Используется для запроса системных разрешений на использование геолокации с помощью
[js-api](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/tap-js-api#пермишены)
в ППЯ и ЯБро. При запросе разрешения браузер показывает нативное окно с переходом в настройки.
Если в разрешении отказано, будет выброшено исключение `GeolocationPermissonError`.
> ⚠️ В ППЯ на iOS системные разрешения работают иначе. Браузер сам запрашивает разрешение на использование геолокации на старте
> всего приложения, если запретить доступ к геолокации после старта и пытаться вызывать js-api, то системное окно не
> будет показано.
```ts
enum PermissionPreset {
  Default = 'default',
  Checkout = 'checkout',
}

type PermissionOptions = {
  onJSApiError?: (error: JSApiError) => void;
  permissionPreset?: PermissionPreset;
};

function requestGeolocationPermissions(options?: PermissionOptions): Promise<void>;
```

### checkGeolocationPermissions

Используется для проверки состояния системного разрешения на использование геолокации с помощью
[js-api](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/tap-js-api#пермишены) в ППЯ и ЯБро.
Если в разрешении отказано, будет выброшено исключение `GeolocationPermissonError`.
```ts
function checkGeolocationPermissions(options?: PermissionOptions): Promise<void>;
```

### getCurrentPosition

Обёртка над `window.navigator.geolocation.getCurrentPosition`.
Перед тем, как получать геопозицию проверяет наличие системного разрешения к геолокации с помощью [checkGeolocationPermissions](###checkGeolocationPermissions).
В случае ошибки в `window.navigator.geolocation.getCurrentPosition` выбрасывается `PositionErrorWrapper`.
```ts
function getCurrentPosition(options?: PositionOptions & PermissionOptions): Promise<GeolocationPosition>
```

### watchPosition

Обёртка над `window.navigator.geolocation.watchPosition`.
Перед тем, как получать геопозицию проверяет наличие системного разрешения к геолокации с помощью [checkGeolocationPermissions](###checkGeolocationPermissions).
В случае ошибки в `window.navigator.geolocation.watchPosition` выбрасывается `PositionErrorWrapper`.
```ts
function watchPosition(callback: PositionCallback, errorCallback: WrappedPositionErrorCallback, options?: PositionOptions & PermissionOptions): Promise<number>;
```

## network
### isNetworkConnectionFailed

Используется для проверки наличия сети с помощью тестового запроса.
```ts
type NetworkAvailableOptions = {
    url: string; // урл запроса, которым будем проверять наличие сети
    method?: 'GET' | 'HEAD' | 'POST';
    timeout?: number // таймаут, по которому перестанем ждать запрос
};

function isNetworkConnectionFailed(options: NetworkAvailableOptions, error: Error): Promise<boolean>;
```

## plural

Возвращает нужное склонение текста для переданного `count`.
```ts
function plural(count: number, messages: string[]): string;
```

## polyfill-checkers
### shouldPolyfillURLSearchParams

Проверяет, нужно ли полифилить `URLSearchParams`, учитывая баги в реализации.
```ts
function shouldPolyfillURLSearchParams(): boolean;
```
