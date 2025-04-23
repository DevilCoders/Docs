# Клиент-серверное взаимодействие

## React-query

[Официальная документация](https://react-query.tanstack.com/overview)

### useQuery

Чтобы получить данные на клиенте мы используем хук `useQuery`
```ts
useQuery(queryKey, queryFn?, options?)
```

Например,
```ts
const categoriesQuery = useQuery('categories', async () => {
    const res = await fetch(`/api/categories/get-categories`);
    return res.json();
});
```

Что происходит?
`useQuery` выполняет функцию, указанную вторым аргументом и ее результат кэширует по ключу `categories`. Если мы вызовем в другом месте `useQuery` с таким же ключом, то запроса не будет, вернутся данные из кэша по ключу.

`categoriesQuery` содержит много полезных полей:
`isLoading`, `isFetching`, `isError` и другие. Смотри [доку](https://react-query.tanstack.com/reference/useQuery).

useQuery принимает третий параметр - конфигурационный. В нем можно указать `staleTime` - время протухания данных, `retry` - количество ретраев и другие. Чтобы не указывать их во всех хуках, указываем их при инициализации `queryClient`.

### Query-client

Мы используем следующий конфиг:
``` ts
{
    defaultOptions: {
        queries: {
            staleTime: Number.MAX_SAFE_INTEGER,
            refetchOnWindowFocus: false,
            retry: 3
        }
    }
}
```

### Используемые фичи

Ключом в useQuery может выступать массив из строк, чисел, объектов
``` ts
useQuery(['categories', { id: categoryId }], ...)
```

#### defaultQueryFn

Чтобы не писать шаблонные функции запроса в `useQuery`, можно задать дефолтную функцию и указать ее в конфиге `queryClient`, и ходить в нужную ручку в зависимости от ключа. Условимся делать ключ массивом из двух элементов:
- первый - это ручка, которую дергаем - строка
- второй - query параметры для нее - объект

``` ts
async function defaultQueryFn({queryKey}) {
    const params = queryKey[1] ? `?${qs.stringify(queryKey[1])}` : '';
    const res = await fetch(`/api/${queryKey[0]}${params}`);

    if (!res.ok) {
        throw new Error('Network response was not ok');
    }

    return res.json();
}
```

Теперь мы можем написать так
``` ts
const categoriesQuery = useQuery(['categories/get-categories', {id: 1}]);
```

### SSR

Так как у нас работает серверный рендеринг, мы рендерим наш интерфейс на сервере и соответственно при рендере тоже дергаются useQuery хуки. Чтобы отрисовать на сервере интерфейс уже наполненный данными, а не лоадерам, и чтобы не запрашивать их на клиенте при заходе на страницу, нужно заранее положить их в кеш, чтобы useQuery сразу вернул данные в момент рендера.

``` ts
queryClient.prefetchQuery('categories/get-categories', getCategories)
```

Затем прокидываем кэш на клиент через `window.__REACT_QUERY_STATE__`.


#### defaultQueryFn

На сервере тоже хочется иметь свою дефолтную функцию. Но в отличие от клиента на сервере мы не будет делать запрос, а будем вызывать соответствующую функцию API, а не ходить куда-то по сети как это делается на клиенте.

``` ts

const handlers = {
    'categories/get-categories': getCategoriesHandler
};

function defaultQueryFn({queryKey}) {
    const handler = handlers[queryKey[0]];

    if (!handler) {
        console.error(`Handler ${queryKey[0]} not found`);
    } else {
        return handler(queryKey[1]);
    }
}
```

Поэтому ключ запроса должен соответствовать пути, по которому расположена ручка, чтобы дефолтная функция смогла заимпортировать соответствующий хэндер и вызвать его с параметрами, переданными в ключе.

По итогу для запроса на сервере просто пишем
``` ts
queryClient.prefetchQuery('categories/get-categories')
```

### Tips and tricks

#### initialData / setQueryData

Предположим, что мы получили список категорий
``` ts
useQuery(['categories/get-categories']);
```

А затем переходим к первой из них, и то что нам нужно отобразить уже получено. Как не делать лишний запрос?

``` ts
useQuery(['categories/get-categories', {id: 1}], {
    initialData: () => queryClient.getQueryData(['categories/get-categories']).find((item) => item.id === id)
});
```

Мы пытаемся найти в кэше по ключу `categories/get-categories`, нужную нам категорию и кладем в `initialData`. Таким образом не будет запроса в начале, т.к. есть данные.

Либо после запросах всех данных, кэшировать их руками.
``` ts
const categories = useQuery(['categories/get-categories']);
useEffect(() => {
    categories.data?.forEach((item) => {
        queryClient.setQueryData('categories/get-categories', {id: item.id}], item)
    });
}, [categories.data]) // Оборачиваем в useEffect, чтобы вызывать setQueryData только при изменении данных

useQuery(['categories/get-categories', {id: 1}]) // теперь есть данные по этому ключу
```
