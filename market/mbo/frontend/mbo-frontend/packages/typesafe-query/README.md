# @yandex-market/typesafe-query

Библиотека для конвертации query параметров URL.

## Особенности

- Поддержка TypeScript
- Типизированная конвертация в объект
- Создание собственных типов

## Установка

```bash
npm install @yandex-market/typesafe-query
```

## Простой пример использования

```typescript
// query-configs.ts
import { createQueryConverter, IQueryConfig, QueryTypes } from '@yandex-market/typesafe-query';

export interface IPagerFilter {
  page: number;
  limit: number;
}

export interface ISortFilter {
  sortField?: string;
  sortOrder?: string;
}

const pagerQueryConfig: IQueryConfig<IPagerFilter> = {
  page: {
    key: 'page',
    type: QueryTypes.number,
    defaultValue: 1,
  },
  limit: {
    key: 'limit',
    type: QueryTypes.number,
    defaultValue: 15,
  },
};

const sortQueryConfig: IQueryConfig<ISortFilter> = {
  sortField: {
    key: 'field',
    type: QueryTypes.string,
  },
  sortOrder: {
    key: 'order',
    type: QueryTypes.string,
    defaultValue: 'asc',
  },
};

export const pagerConverter = createQueryConverter(pagerQueryConfig);

export const sortConverter = createQueryConverter(sortQueryConfig);

// some-file.ts
import { parse, stringify } from 'query-string';
import { pagerConverter, sortConverter } from './query-configs';

const search = 'page=23&field=name';
const parsed = parse(search); // -> { page: "23", field: "name" }

pagerConverter.decode(parsed); // -> { page: 23, limit: 15 }
sortConverter.decode(parsed); // -> { sortField: 'name', sortOrder: 'asc' }

pagerConverter.encode({ limit: 50, page: 10 }); // -> { limit: "50", "page": "10" }
sortConverter.encode({ sortField: 'name', sortOrder: 'desc' }); // -> { filed: "name", "order": "desc" }

stringify({
  ...pagerConverter.encode({ limit: 50, page: 10 }),
  ...sortConverter.encode({ sortField: 'name', sortOrder: 'desc' }),
}); // -> ?limit=50&order=desc&page=10&field=name
```

Библиотека также предоставляет вспомогательные функции для описания типов:

#### Пример с использованием `QueryTypes`

```typescript
import { IQueryConfig, QueryTypes } from '@yandex-market/typesafe-query';

const config: IQueryConfig = {
  str: {
    type: QueryTypes.string,
    defaultValue: 'default string',
  },
  num: {
    type: QueryTypes.number,
    defaultValue: 1,
  },
  bool: {
    type: QueryTypes.boolean,
    defaultValue: false,
  },
  json: {
    type: QueryTypes.json,
    defaultValue: {},
  },
  arrStr: {
    type: QueryTypes.arrayOf(QueryTypes.string),
    defaultValue: ['one', 'two', 'three'],
  },
  arrNum: {
    type: QueryTypes.arrayOf(QueryTypes.number),
    defaultValue: [1, 3, 5],
  },
  arrBool: {
    type: QueryTypes.arrayOf(QueryTypes.boolean),
    defaultValue: [true, false, false],
  },
};
```

### Пример с использованием `QueryArgs`

```typescript
import { IQueryConfig, QueryArgs } from '@yandex-market/typesafe-query';

const config: IQueryConfig = {
  str: QueryArgs.string('default string'),
  num: QueryArgs.number(1),
  bool: QueryArgs.boolean(false),
  json: QueryArgs.json({}),
  arrStr: QueryArgs.arrayOfString(['one', 'tow', 'three']),
  arrNum: QueryArgs.arrayOfNumber([1, 3, 5]),
  arrBool: QueryArgs.arrayOfBoolean([true, false, false]),
};
```

## Создание типов

На самом деле тип - это простой объект, который имеет 2 свойста: `encode` и `decode`.

Пример создания типа:

```typescript
import { createHelperArrayType, createHelperType, IQueryConfig, IQueryType } from '@yandex-market/typesafe-query';

enum SortOrder {
  ASC = 'ASC',
  DESC = 'DESC',
}

// Для создания типа необходимо описать 2 функции в объекте: encode и decode
const QueryTypeSortOrder: IQueryType<SortOrder> = {
  /**
   * Функция для конвертации значения в query параметр
   */
  encode: order => (order == null ? undefined : String(order)),
  /**
   * Функция для конвертации query параметра в значение
   */
  decode: orderStr => {
    if (typeof orderStr === 'string') {
      if (orderStr === SortOrder.ASC) {
        return SortOrder.ASC;
      }

      if (orderStr === SortOrder.DESC) {
        return SortOrder.DESC;
      }
    }

    // Если вернуть undefined, то в конечном объекте
    // в качестве значения будет значение по умолчанию (если оно указано)
    return undefined;
  },
};

// Также можно воспользоваться функцией для создания вспомогательной функции типа:
const sortOrderType = createHelperType(QueryTypeSortOrder);

const config: IQueryConfig = {
  sortOrder: sortOrderType(SortOrder.ASC),
};

// Для создания вспомогательной функции для массива, лучше использовать `createHelperArrayType`
const customArrayType = createHelperArrayType(QueryTypeSortOrder);
```
