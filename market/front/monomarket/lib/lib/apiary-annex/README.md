[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/lib/apiary-annex)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/lib/apiary-annex) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/apiary-annex)](https://oko.yandex-team.ru/pkg/@yandex-market/apiary-annex)

### apiary-annex


- [Общие компоненты](https://github.yandex-team.ru/market/apiary-annex)
- [Общие виджеты](https://github.yandex-team.ru/market/apiary-annex/tree/master/src)
- [Обработчики общих джоб (cookie, meta, title, redirect, status)](https://github.yandex-team.ru/market/apiary-annex/tree/master/src/jobs)

## Джобы

Рассмотрим общие джобы, определённые в `apiary-annex`.

### `titleJob`

Джоба для выставления `<title>`. Игнорируются все джобы от виджетов, не лежащих на main-пути. Первая джоба выставляется в блокирующем режиме, потом отложенно выставляется последняя.

```js
import {titleJob} from '@yandex-market/apiary-annex/jobs';

titleJob(Promise.resolve('some <title> content'))
titleJob(Promise.resolve(null)) // отменить выставление заголовка
```

### `metaJob`

Джоба для выставления метаинформации (`<meta>`). Результирующая мета получается смёрживанием всех джоб виджетов на main-пути. Метаинформация выставляется только при отдаче роботу.

```js
import {metaJob} from '@yandex-market/apiary-annex/jobs';

metaJob({
    type: Promise.resolve('website'),
    title: Promise.resolve('Гвозди'),
    description: Promise.resolve('Какие-то гвозди'),
    canonical: Promise.resolve(['somePageId', {...}])
    publishedTime: Promise.resolve(new Date('2017-08-24')),
    images: Promise.resolve(['//yastatic.net/market-export/_/i/market-icon.png']),
    prevPage: Promise.resolve(['somePageId', {...}]),
    nextPage: Promise.resolve(['somePageId', {...}]),
    robots: Promise.resolve({index: false, follow: true}),
})
```

### `cookieJob`

Джоба для выставления кук. Все куки выставляются в отложенном режиме, с клиента. Все куки, перечисленные в джобе выставляются атомарно.
Доступные опции см. в [jshttp/cookie](https://github.com/jshttp/cookie)

```js
import {cookiesJob} from '@yandex-market/apiary-annex/jobs';

cookiesJob({
    'some-cookie': Promise.resolve('1'),
    'another-cookie': Promise.resolve(['1', {maxAge: 24 * 60 * 60}]),
    'cancel': Promise.resolve(null), // отменить выставление куки
})
```

### `redirectJob`

Джоба для совершения редиректа. Выполняется редирект для последней выставленной джобы от виджета на main-пути.

```js
import {redirectJob} from '@yandex-market/apiary-annex/jobs';

redirectJob(Promise.resolve(['somePageId', {...}]))
redirectJob(Promise.resolve([['somePageId', {...}], 301])
redirectJob(Promise.resolve('url'))
redirectJob(Promise.resolve(['url', 301]))
redirectJob(Promise.resolve(null)) // не совершать редирект
```

### `statusJob`

Джоба для выставления статуса ответа. Выставляется последний статус от виджетов на main-пути. Выполняется только для роботов.

```js
import {statusJob} from '@yandex-market/apiary-annex/jobs';

statusJob(Promise.resolve(508))
statusJob(Promise.resolve(null)) // отменить выставление статуса
```
