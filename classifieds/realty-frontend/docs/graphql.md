# Про работу с Graphql

Ссылки
* [Песочница](http://realty-graphql-server-api.vrts-slb.test.vertis.yandex.net/playground)
* [Локальный playground](https://a.yandex-team.ru/arcadia/classifieds/realty-frontend/realty-core/app/graphql/playground.ts)
* [Ручка в gateway](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x#!/graphql/graphQL)

## Флоу работы

1) Добавляем query / mutation в [operations](https://a.yandex-team.ru/arcadia/classifieds/realty-frontend/realty-core/app/graphql/operations/)
2) Валидируем запросы и генерируем типы через `make gql-generate-types `, команда добавит `.generated.ts` файлы рядом с запросами
3) Используем на nodejs запросы через `this.req.graphql.request` в Gate / Controller
4) На клиенте используем сгенерированные типы

Пример:

```ts
// GetOffer.ts
import { gql } from 'graphql-tag';

export const GetOffer = gql`
    query GetOffer($offerId: String!) {
        offer(offerId: $offerId) {
            offerId
            offerType
            ...
        }
    }
`;
```

`graphql-tag` необходим, чтобы распарсить в AST graphql, парсим, чтобы достать из запроса полезную информацию

```ts
// PageController
const response = await this.req.graphql.request(
    GetOffer,
    { offerId: '199780306372749824' },
    { isMandatory: true, timeout: 500, maxRetries: 1 }
);
```

```ts
// types.ts (на клиентской части)
import { GetOfferQuery } from 'realty-core/app/graphql/operations/queries/realty/GetOffer.generated';

interface IOffer extends GetOfferQuery {}
```

## Best practice

1) Если есть переиспользуемые части полей в сущностях, то их лучше выносить во [фрагменты](https://graphql.org/learn/queries/#fragments)
