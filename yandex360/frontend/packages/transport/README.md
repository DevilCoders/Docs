# PS-transport
![npm stable version](https://badger.yandex-team.ru/npm/@ps-int/transport/version.svg)

JSON-RPC client-side library targeting compatibility with Duffman.

## Example usages

### Configuration
```typescript
import { Model, ModelsApi, Logger, ModelResult } from '@ps-int/transport';

interface DataItem {
    id: string;
    name: string;
    value: string;
}

enum ModelNames {
    getList = 'get-list',
    getItem = 'get-item',
    doSetItem = 'do-set-item'
}

type Models = {
  [ModelNames.getList]: Model<{}, Array<DataItem>>
  [ModelNames.getItem]: Model<{ id: string; }, DataItem>
  [ModelNames.doSetItem]: Model<DataItem, { ok: boolean; }>
};

interface ApiError extends Object {}

class ErrorReporter implements Logger {
    logError(error: Error) {
        // some actions to log error
    }
}

// service-specific headers needed for particular api endpoint
function getAdditionalHeaders() {
    return {
        'x-yandex-ckey': 'ckey_value',
        'x-yandex-uid': 'uid_value',
    };
}

// service-specific body fields needed for particular api endpoint
function getAdditionalBodyFields() {
    return {
        '_exp': 'experiments_string_value',
        '_eexp': 'applied_experiments_value',
    };
}

const api = new Api(
    'https://mail.yandex.ru/web-api/_m',
    {
        getAdditionalHeaders,
        getAdditionalBodyFields
    },
    new ErrorReporter()
);

const modelsApi = new ModelsApi<Models>(
    api,
    {
        modelsQueryParameter: '_models',
    }, 
);
```

### Fetch single model
```typescript
modelsApi.requestModelsTuple([{ name: ModelNames.getList, params: {} }]).then((result) => {
    if (modelsApi.isModelResolved(result[0])) {
        const items = result[0].data;
    }
});
```

### Fetch undefined amount of model
```typescript
const itemIds = ['123', '456', '789', '234']; // Some runtime dynamic value
const modelsToFetch: GetModelRequestParams<Models, ModelNames.getItem>[] = itemIds.map(id => ({ name: ModelNames.getItem, params: { id } }));

modelsApi.requestModelArray(modelsToFetch).then((result) => {
    result.forEach(r => {
        if (modelsApi.isModelResolved(r)) {
            r.data.id
        }
    })
});
```

### Set something and get the result back
```typescript
const item: DataItem = {
    id: '123',
    name: 'some-cool-item',
    value: '42'
};
const setItemParams = [
    { name: ModelNames.doSetItem, params: item },
    { name: ModelNames.getItem, params: { id: item.id } }
] as const;

modelsApi.requestModelsTuple(setItemParams).then((result) => {
    const [_setItemResult, itemModel] = result;
    if (modelsApi.isModelResolved(itemModel)) {
        const updatedItem = itemModel.data;

        // do something with updated item
    }
});
```

### Error handling
```typescript
const itemsRequestParams = [
    { name: ModelNames.getItem, params: { id: '123' } },
    { name: ModelNames.getItem, params: { id: '456' } }
] as const;

modelsApi.requestModelsTuple(itemsRequestParams).then((result) => {
    result.forEach((modelResult) => {
        // and vice versa, 'modelsApi.isModelResolved(modelResult)' is available
        if (modelsApi.isModelRejected(modelResult)) {
            // handle error

            return;
        }

        const item = modelResult.data;
        // handle successful model response
    });
});
```

### Interceptors
#### Response

[Подробное описание interceptor](src/interceptors/README.md)

```typescript
import { makeLogErrorInterceptor } from '@ps-int/transport/interceptors';

const logModelsErrorInterceptor = makeLogErrorInterceptor<Models>((error) => {
    // some actions to log model error
});
    
const modelsApi = new ModelsApi<Models>(
    api,
    {
        modelsQueryParameter: '_models'
    },
    {
        response: logModelsErrorInterceptor
    }
);
```

## Development

### Publish version

```bash
npm run package X.Y.Z
```
Command updates `package.json` version, commits version changes, puts a version tag on
this commit, publishes resulting package to NPM and pushes everything to Github.
