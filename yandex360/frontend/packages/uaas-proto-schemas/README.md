# @ps-int/uaas-proto-schemas

Proto-схемы для УАЗ

```(bash)
npm i -S @ps-int/uaas-proto-schemas protobufjs
```

```(javascript)
const {
    TUaasRequest,
    TUaasResponse
} = require('@ps-int/uaas-proto-schemas');

const uaasRequest = {
    UsersplitRequestParams: {
        Experiments: {
            AddExperiments: [
                '12345'
            ]
        },
        Timestamp: Date.now(),
        Ip: '1.2.3.4',
        Restrictions: {
            Service: 'mail'
        },
        SplitIds: {
            Uuid: 'deadbeef'
        }
    }
};

const { body } = await got.post('http://uaas.search.yandex.net/__protobuf__', {
    method: 'POST',
    encoding: null,
    body: TUaasRequest.encode(TUaasRequest.fromPartial(uaasRequest)).finish()
});

const uaasResponse = TUaasResponse.decode(Buffer.from(body));
const { TestBucket, RawHandlers } = uaasResponse.Experiments[0];
```

## обновить схемы

```(bash)
npm run update
```
