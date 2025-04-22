# Как добавить моки

Для моков используется низкоуровневая функция типа `MockRequest`, использующая в качестве аргументов те же типы, что и `request`.

```ts
type MockRequest<T, Q> = (req: BasicRequest, options: RequestOptions<T, Q>) => Promise<RequestResponse<T>>;
```

## Добавление новых серверных моков

Для добавления новых серверных моков требуется добавить в `request` параметр `mockRequest` типа `MockRequest`.

Для использования s3 хранилища рекомендуется использовать стратегию `s3ServerMock` из модуля `server/mocks/mock-strategies`. В качестве первого аргумента стратегия принимает ключ хоста, оно должно совпадать с ключом хоста, в который запрос ходит без моков. Второй аргумент стратегии `S3MockStrategyOptions` описан ниже.

## Добавление новых клиентских моков

Для добавления новых клиентских моков необходимо добавить пару `ключ клиентского хоста - MockRequest` в объект `hosts` в `server/mocks/client-hosts-mocks.ts`.

Для использования s3 хранилища рекомендуется использовать стратегию `s3ClientMock` из модуля `server/mocks/mock-strategies`. В качестве первого аргумента стратегия принимает ключ хоста, оно должно совпадать с ключом хоста, в который запрос ходит без моков. Второй аргумент стратегии `S3MockStrategyOptions` описан ниже.

## Опции стратегии `S3MockStrategyOptions`

-   `format` - формат данных, будет использован как расширение при сохранении мока.
-   `getKey` - функция, вычисляющая уникальный id мока по параметрам запроса. Тут стоит использовать все данные, изменение которых влияет на изменение ответа. Например, для маршрутов сюда стоит занести точки маршрута и режим, но не надо заносить часовой пояс клиента.

# Примеры

## Возврат постоянного значения

```ts
import {BASE64_COLORS} from 'server/mocks/mock-utils';

interface TileOptions {
    l?: string;
}

const TILE_MOCK: MockRequest<string, TileOptions> = (_req, options) => {
    const isSatellite = options.query.l === 'sat';
    if (isSatellite) {
        return BASE64_COLORS.blue;
    }
    return BASE64_COLORS.green;
};
```

## Модификация возвращаемого значения

```ts
import {s3ServerMock, modifyResponse} from 'server/mocks/mock-strategies';

interface ResponseType {
  lastUpdated: number;
  ...
}

const RAW_SERVER_MOCK = s3ServerMock('inthostKey', {
  getKey: ({query}) => [query.x, query.y]
});

const SERVER_MOCK = modifyResponse(
  RAW_SERVER_MOCK,
  // data - возвращаемое значение
  (data, req) => {
    data.lastUpdated = new Date();
  }
)
```

# Отладка моков

Для отладки моков используется локальное хранилище (файлы находятся в `/.s3/`).
