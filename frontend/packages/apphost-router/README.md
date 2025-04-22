# apphost-router

Набор классов для того, чтобы обработка запросов с `@yandex-int/apphost-lib` была более похожа на express.
Тем не менее, всё-таки имеются существенные отличия, обусловленные всеядностью аппхоста:
- т.к. нет "запроса", и вообще не факт, что обрабатывается http request, то матчинг урлов вынесен отдельно в `HttpRequestParser`
- т.к. чтение чанков из контекста тоже не обязательно будет одним куском, то `HttpRequestParser` нужно явно просить распарсить http-запрос.
- т.к. ответ тоже не обязательно будет единственным и не обязательно в виде http response, то в параметрах нет никакого res, но есть ctx чтобы  можно было отправить что-нибудь в контекст
- пока что нет возможности делать вложенные роутеры (при необходимости это можно реализовать)

Кроме того, несмотря на то, что `@yandex-int/apphost-lib` не ограничивает вас в выборе между `protobufjs` и `google-protobuf`, в этом пакете все Http зависимые классы используют `protobufjs`.

Содержит 4 компонента
  - [ApphostRouter](#apphostrouter)
  - [HttpRequestParser](#httprequestparser)
  - [ResponseSender](#responsesender)
  - [StaticSender](#staticsender)

## ApphostRouter

Служит основой, в которую добавляются middleware, которые обрабатывают запрос.
Middleware - функция, которая  возвращает (сразу или в промисе) `true|false` и принимает 2 параметра (3 для обработчика ошибок):
- `req` - объект, связанный с запросом.

   Изначально это пустой EventEmitter, отправляющий единственное событие `finish` при завершении обработки запроса.
- `ctx` - [аппхостовый контекст](https://docs.yandex-team.ru/apphost/pages/api_nodejs#protobufjscontext)
- `error` - ошибка для обработчика ошибок

Для добавляения middleware есть 2 метода:
- `use` добавляет обычные middleware, которые которые будут вызываться по порядку, пока какой-нибудь из них не вернёт `true`
- `error` добавляет обработчики ошибок

Для связи с `@yandex-int/apphost-lib` нужно передать метод `handler` параметром в нужный `addHandler`.

Пример:
```js
import {Service, ServiceTransport} = from '@yandex-int/apphost-lib';
import {ApphostRouter} from '@yandex-int/apphost-router';

const app = new ApphostRouter();

app
    .use(async (req, ctx) => {
        // обычный middleware

        req.once('finish', () => {
            // выполнится после того, как обработка завершится.
            // здесь можно, например, залогировать время работы
        });

        if (...) {
            // завершили запрос
            return true;
        }

        // передали запрос следующему middleware
        return;
    })
    .error((req, ctx, e) => {
        // обработчик ошибок
        if (...) {
            // обработали ошибку и завершили запрос
            return true;
        } else if (...) {
            // обработали ошибку и передали запрос следующему middleware
            return;
        }
        // передали запрос следующему обработчику ошибок
        throw e;
    });

Service
    .create({transport: ServiceTransport.GRPC})
     /* обрабатываем роутером запросы в хендлере /some
      * Это хэндлер вашего бэкенда, а не http путь исходного запроса
      */
    .addHandler('/some', app.handler);
```

### Обработка ошибок
1. Если middleware завершилась с ошибкой, то будет вызван обработчик ошибок, объявленный после этой middleware.
2. Обработчик ошибок должен завершиться одним из 3 способов
    - вернуть `true` и таким образом завершить обработку этого _запроса_,
    - вернуть `false` и таким образом передать обработку _запроса_ следующей _middleware_,
    - бросить полученую ошибку и таким образом передать обработку _ошибки_ следующему _обработчику ошибок_.

    **NB** Обработка запроса сразу же завершится ошибкой, если обработчик ошибки выбросит любую иную ошибку, кроме переданой.


## HttpRequestParser

Класс для работы с http запросом. Класс помогает добавлять middleware, зависящие от http пути исходного запроса. Кроме того, он представляет http запрос в более удобном виде (Например, заголовки представлены в виде объекта с нормализоваными именами).

При создании объекта требуется передать функцию, которая вернёт THttpRequest (protobufjs объект, полученый из протобуфа по [этой схеме](../../../web/app_host/lib/proto_answers/http.proto))
В простейшем случае подойдёт такой код
```js
const http = new HttpRequestParser(async(req, ctx) => {
    // читаем все чанки из контекста
    const chunks = await ctx.allIncomingChunks();
    // парсим сущность с именем request по схеме
    return chunks.getOnlyItem('request').parseProto(NAppHostHttp.THttpRequest);
});

```

Перед тем, как осуществлять роутинг, нужно добавить в роутер middleware, которая распарсит http запрос
```js
app.use(http.parse); // переданная в конструкторе функция будет вызвана в этом middleware
```
Парсинг сделан отдельно потому что мы не всегда обрабатываем именно http запрос и не всегда его нужно парсить в первую очередь.

После парсинга `req` будет дополнен свойствами:
- `method` Метод запроса (`Get`, `Post`, `Put`, и т.д.)
- `scheme` схема запроса (`http`, `https`, `none`)
- `secure` получен ли запрос от пользователя по https (т.е. `scheme` равна `https` или есть заголовок `X-Yandex-Https: yes`)
- `hostname` содержимое заголовка `Host`
- `headers` объект с заголовками запроса. названия заголовоков приведены к нижнему регистру.
- `url` путь запроса вместе с query
- `path` нормализованый путь запроса (нормализация производится функцией из пакета [path](https://nodejs.org/api/path.html#path_path_normalize_path)
- `query` павраметры запроса в виде [URLSearchParams](https://nodejs.org/api/url.html#url_class_urlsearchparams)
- `content` тело запроса в виде Uint8Array

И можно использовать роутинг по http путям
```js
app.use(http.match('/some/path', (req, ctx) => {
    /* сюда попадём только при полном совпадении нормализованого
     * пути со строкой /some/path без учёт регистра
     */
}));
```
Роутинг по путям можно использовать и для обработчиков ошибок тоже:
```js
app.use(http.match(/^\/some\/prefix/, (req, ctx, e) => {
    if (e.code === 'ENOENT') {
        // вернём 404
    }
    throw e;
}));
```

## ResponseSender

Класс для упаковки ответов в протобуф и отправки в контекст. Призван сократить количество копипасты, когда нужно отправлять однотипные ответы.

При создании принимает в параметрах имя, под которым ответ будет отправлен в контекст и protobufjs энкодер/декодер, которым ответ будет упакован перед отправкой.

Экземпляр имеет единственный метод wrap, которым нужно обернуть middleware, которая будет возвращать объект для отправки:
```js
const sender = new ResponseSender('res', NAppHostHttp.THttpResponse);

app.use(sender.wrap((req, ctx) => {
    if (...) {
        // передали запрос следующему middleware
        return;
    }
    /* Возвращаем объект, а не boolean.
     * Объект буден упакован в NAppHostHttp.THttpResponse
     * и отправлен в контекст под именем res
     */
    return {
        StatusCode: 404,
        Headers: [
            {
                Name: 'Content-type',
                Value: 'text/html'
            }
        ],
        Content: Buffer.from('<h1>404 Not found</h1>')
    };
}));
```
Можно использовать при обработке ошибок и комбинировать с HttpRequestParser'ом
```js
app.error(sender.wrap((req, ctx, e) => {
    if (e.code === 'ENOENT') {
        return {
            StatusCode: 404,
            Content: Buffer.from('Not found')
        };
    } else {
        return {
            StatusCode: 503,
            Headers: [
                {
                    Name: 'Content-type',
                    Value: 'text/html'
                }
            ],
            Content: Buffer.from(`<h1>Internal error</h1>
                <p>
                    ${
                        process.env.DEV ? e.stack : ''
                    }
                </p>`)
        };
}));
app.use(http.match('/ok.html', sender.wrap(() => {
    return {
        StatusCode: 200,
        Content: Buffer.from('ok')
    }
})));
```

## StaticSender

Класс для отправки статики. Читает файлы из диска в память, отдаёт ответ из памяти. Как и соортветствующий модуль из extress'а, умеет определять Content-type файла, проставляет заголовок `Last-Modified` и учитывает на заголовок `If-Modified-Since` в запросе (если запрос был обработан HttpRequestParser'ом).

Тем не менее очень хорошо подумайте, прежде чем использовать связку apphost + nodejs для раздачи статики, т.к. раздача статики с cdn или с отдельностоящего (не под аппхостом) nginx'а гарантированно будет быстрее/надёжнее/экономнее по ресурсам.

Для чтения файлов в память экземпляр класса имеет 2 метода
### addFile
Читает один конкретный файл.
Параметры
- `url` точный урл, по которому файл нужно отдавать
- `file` точный  путь до файла на файловой системе
- `opts` объект с опциями
- `opts.stat` объект `fs.Stat` для этого файла
- `opts.headers` массив с заголовками по [этой схеме](../../../web/app_host/lib/proto_answers/http.proto). Среди этих заголовков **не должно быть** `Date`

### addDir
Читает все файлы в директории рекурсивно, кроме начинающихся с точки.
Параметры
- `urlPrefix` префикс урла, на который будет матчится директория
- `dir` точный путь до директории на файловой системе
- `opts` объект с опциями аналогично `addFile`

Помимо этого, есть дополнительные методы
### setHeaders
Позволяет установить отдельные заголовки для урла.
- `url` точный урл
- `headers` заголовки в виде, аналогичном `opts.headers`

### getInfo
Возвращает объект с информацией о размере всех прочитанных файлов

### handler
Представляет middleware, которую нужно поместить в роутер.
Его всегда нужно оборачивать ResponseSender'ом, которые упакует и отправит ответ под нужным именем.
Естественно его можно использовать в обработчике ошибок и комбинировать с HttpRequestParser'ом.

Пример
```js
const staticSender = new StaticSender();

staticSender.addFile('/favicon.png', './public/favicon.png');
staticSender.addDir('/service-workers/', './public/workers', {
    headers: [
        {
            Name: 'Cache-Control',
            Value: 'public, max-age=5400, no-transform'
        }
    ]
});
staticSender.setHeaders('/service-workers/instant.js', [
    {
        Name: 'Cache-Control',
        Value: 'public, max-age=50, no-transform'
    }
]);

app.use(http.match('/favicon.png', sender.wrap(staticSender.handler)));
app.use(http.match(/^\/service-workers\//, sender.wrap(staticSender.handler)));
```

## Советы по использованию этого пакета
1. Ещё раз подумайте над минусами, прежде чем использовать `StaticSender`
   - требуется все файлы держать в памяти
   - весь файл сначала упаковывается в протобуф, а затем отправляется одним куском
   - менее гибко настраивается, чем nginx
2. Всегда ставьте `match` первым в цепочке, если используете несколько обёрток


   ```js
   // так будет работать, но не надо
   app.use(sender.wrap(http.match('/qwe', staticSender.handler)));

   // лучше так
   app.use(http.match('/qwe', sender.wrap(staticSender.handler)));
   ```
