# @yandex-market/react-typesafe-query

Библиотека работы с параметрами запроса в компонентах React.

## Особенности

- Поддержка TypeScript
- Типизированные параметры запроса
- Частичное обновление параметров запроса

## Установка

Для работы библиотеки необходимо использовать `history@4` и `@yandex-market/typesafe-query`.

```bash
npm install history@4 @yandex-market/typesafe-query
```

```bash
npm install @yandex-market/react-typesafe-query
```

## Простой пример использования

1. Подключаем QueryParamsProvider:

```tsx
import React, { FC } from 'react';
import { History } from 'history';
import { QueryParamsProvider } from '@yandex-market/react-typesafe-query';

export interface IAppProps {
  history: History;
}

export const App: FC<IAppProps> = ({ history, children }) => (
  <QueryParamsProvider history={history}>{children}</QueryParamsProvider>
);
```

2. Оборачиваем нужный компонент в HOC:

```tsx
import React from 'react';
import { IQueryConfig, QueryTypes } from '@yandex-market/typesafe-query';
import { IQueryParamsComponentProps, withQueryParams } from '@yandex-market/react-typesafe-query';

interface IPagerQuery {
  page: number;
  limit: number;
}

const pagerQueryConfig: IQueryConfig<IPagerQuery> = {
  page: {
    type: QueryTypes.number,
    defaultValue: 1,
  },
  limit: {
    type: QueryTypes.number,
    defaultValue: 25,
  },
};

const withPager = withQueryParams(pagerQueryConfig);

export type IPagerProps = IQueryParamsComponentProps<IPagerQuery>;

export const Pager = withPager(({ queryParams, onChangeQueryParams }) => {
  return (
    <div>
      <span>Current: {queryParams.page}</span>
      <button onClick={() => onChangeQueryParams({ page: queryParams.page - 1 })}>Prev</button>
      <button onClick={() => onChangeQueryParams({ page: queryParams.page + 1 })}>Next</button>
    </div>
  );
});
```

`onChangeQueryParams` также вторым аргументом принимает значения `'push' | 'replace' | 'pushIn' | 'replaceIn'`.

- `'push'` - обновляет все параметры запроса и увеличивает длину историю в браузере
- `'replace'` - обновляет все параметры запроса и не увеличивает длину историю в браузере
- `'pushIn'` - объединяет параметры запроса с текущими и увеличивает длину историю в браузере
- `'replaceIn'` - объединяет параметры запроса с текущими и не увеличивает длину историю в браузере

Также может понадобиться настроить, например, конвертацию для массивов. Так как, под капотом используется библиотека [query-string](https://www.npmjs.com/package/query-string), то подробнее о настройках можете почитать [здесь](https://github.com/sindresorhus/query-string).

По умолчанию внутри библиотеки `query-string` заданы следующие настройки:

### ParseOptions

```javascript
{
  // Включить декодирование ключей и значений (decodeURIComponent)
  decode: true,
  // Формат массива. Например, строка `a=1&a=2` будет преобразована в `{ a: ['1', '2'] }`
  arrayFormat: 'none',
  // Сортирует ключи
  sort: true,
  // Пытается преобразовать string в number
  parseNumbers: false,
  // Пытается преобразовать string в boolean
  parseBooleans: false,
}
```

### StringifyOptions

```javascript
{
  // Включение строгого режима кодирования компонентов URI с помощью `strict-uri-encode`.
  strict: true,
  // Включить кодирование ключей и значений (encodeURIComponent)
  encode: true,
  // Формат массива. Например, объект `{ a: ['1', '2'] }` будет преобразован в `a=1&a=2`
  arrayFormat: 'none',
  // Сортирует ключи
  sort: true,
}
```

Подробнее про настройки `query-string` можно почитать [здесь](https://github.com/sindresorhus/query-string#api)

Задать настройки можно в `QueryParamsProvider`:

```tsx
const parseOptions = {
  arrayFormat: 'index',
};
const stringifyOptions = {
  arrayFormat: 'index',
};

return (
  <QueryParamsProvider history={history} parseOptions={parseOptions} stringifyOptions={stringifyOptions}>
    {children}
  </QueryParamsProvider>
);
```
