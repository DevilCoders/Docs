# Interceptors
## Response

Используются для перехвата ответа моделей в случаях, когда есть необходимость совершить дополнительные действия или дополнительную обработку ответа на уровне modelsApi.

Interceptor — это функция, принимает 3 аргумента:
- параметры и ответы моделей InterceptorModel[],
- инстанс ModelsApi
- raw-ответ ApiResponse;

возвращает Promise, который должен резолвиться с InterceptorModel[].

### Фабрики базовых interceptor

Поверх базового api interceptor есть несколько фабрик для создания частоиспользуемых interceptor:
#### cookieRenew
Обновляет куки через iframe. 

Параметры:
- passportAuthUpdateUrl - URL паспорта для обновления куки. Например https://passport.yandex.ru/auth/update
- getShouldRenewCookie (необязятельный) - вычисляет необходимость обновления куки из ответа моделей

#### logError
Логирует ошибку для каждой ModelRejected в ответе.

Параметры:
- logError - функция для логирования ошибки

#### redirect
Редиректит на указанный URL, в случае если checker вернет true

Параметры:
- checker - функция для проверки ModelResult. Если вернет true хоть для одной модели произойдет редирект
- getURL - функция для получения url для редиректа

```typescript
const redirectInterceptor = makeRedirectInterceptor((modelResult, modelsApi) => {
    if (modelsApi.isModelRejected(modelResult)) {
        if (typeof modelResult.error === 'string') {
            return modelResult.error === errorCode;
        }

        if ('code' in modelResult.error) {
            return modelResult.error.code === errorCode;
        }
    }

    return false;
}, getUrl);
```

Поверх написан PassportAuthRedirectInterceptor
```typescript
const passportAuthRedirectInterceptor = makePassportAuthRedirectInterceptor<Models>(
    'https://passport.yandex.ru',
    'AUTH_NO_AUTH'
);
```

#### retry
Ретраит часть моделей

Параметры:
- retryChecker - функция проверяет нужно ли ретраить конкретную модель. Модель, для которой вернется true будет ретраена.
- defaultParams - параметры ретрая для случаев, когда они не переданы в запросе 
    - maxCount - максимальное количество ретраев
- beforeRetry - функция, которая будет выполнена до всех проверок

```typescript
const retryOnCkeyUpdateInterceptor = makeRetryInterceptor<Models>(
    (model, modelsApi) => {
        // Выбираем какие модели ретраить
        if (modelsApi.isModelRejected(model.result)) {
            return model.result.error === 'ckey';
        }

        return false;
    },
    {},
    async (response) => {
        if (response.ckey) {
            setCkey(response.ckey);
        }

        return;
    }
);
```

### Композиция
ModelsApi принимает один interceptor, но можно воспользоваться composeResponseInterceptors для композиции нескольких.
```typescript
const responseInterceptor = composeResponseInterceptors(
    retryOnCkeyUpdateInterceptor,
    passportAuthRedirectInterceptor,
    logModelsErrorInterceptor
)
```
