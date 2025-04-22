# OAuth

## Состояние прода

![Production Errors Graph](http://gr.yandex-team.ru/render?width=640&from=-24h&until=now&height=360&title=OAuth.%20Front-end%20errors%20(Sum%20All%20DC%20per%205min)&_comment=&areaMode=none&vtitle=count%20per%205min&hideLegend=false&xFormat=%25H%3A%25M&target=cactiStyle(alias(sumSeries(portal.passport.oauth.oauth-%7Bu6%2Ci%2Cm%2Cna%2Cnb%2Cs%7D%5B1-9%5D.oauth.nodejs.critical)%2C%20'Critital'))&target=cactiStyle(alias(sumSeries(portal.passport.oauth.oauth-%7Bu6%2Ci%2Cm%2Cna%2Cnb%2Cs%7D%5B1-9%5D.oauth.nodejs.error)%2C%20'Error'))&target=cactiStyle(alias(sumSeries(portal.passport.oauth.oauth-%7Bu6%2Ci%2Cm%2Cna%2Cnb%2Cs%7D%5B1-9%5D.oauth.nodejs.warn)%2C%20'Warning')))

## Ответ на запрос

1. [Рутер][Router] подбирает инстанс [Страницы][Page], соответствующий текущему урлу.
2. Страница инициализируется с инстансом [Контроллера][Controller] для доступа к объектам `request` и `response` экспресса,
   и [Апи][Api] для взаимодействия с бэкендом.
3. У страницы вызывается метод `open`, и с этого момента контроль целиком переходит к странице.
4. Страница [рендерит](#Отрисовка страницы) и отсылает ответ


## Отрисовка страницы

Чтобы отрисовать страницу, нужно создать [Лэйаут][Layout].
Лэйаут наследуется от [CompositeView], который наследуется от [View].

Чтобы получить html нужно у инстанса Лэйаута вызвать метод `render`.
Лэйаут скомпилирует JSON для шаблонизации и передаст его в шаблонизатор.
```javascript
var layout = new Layout();
layout.render(); //Вернет промис, который зарезолвится с html'кой
```
 
К лэйауту можно подключать любое количество [View],
они будут так же скомпилированы и переданы в шаблонизатор для рендеринга:
 
```javascript
var ArbitraryView = inherit(View, {
    _compile: function() {
        return { arbitraryData: 'asdf' };
    }
});

layout.append(new ArbitraryView())
layout.compile(); 
```
Результатом вызова к `layout.compile()` будет промис, который зарезолвится с объектом,
в поле `page` будет лежать `arbitraryData: 'asdf'`

Именно тот объект, с которым резолвится `compile` Лэйаута становится данными для шаблонизации.


### Шаблон страницы

Лэйаут передает в ять JSON с тремя полями: `config`, `meta`, и `page`.

В `config` лежит информация о том, откуда забирать статику, и прочая конфигурация.

В `meta` лежит глобальная информация о запросе:
язык, урл (с доменом и tld), идентификатор лога, переменная окружения.

В `page` попадают данные, специфичные для отрисовки страницы.
Все скомпилированные View, которые были добавлены к Лэйауту окажутся именно здесь.

Каждый шаблон страницы должен определять функцию `page-content(nodeset page, nodeset meta, nodeset config)`.
Эта функция определяет что окажется на странице.


## Как трансформировать ответ сервера для более удобной работы?

Если ты хочешь перманентно поменять ответ сервера, то ты идешь в [Апи][Api] и трансформируешь ответ в then-callback'е ручки, которая ходит в бэкенд за данными.

Большинство ручек возвращают инстансы [Моделей][Models], можно править их методы. Например, [клиент][ClientModel] возвращает 1970 год, если не `create_time: null`

Если ты хочешь в конкретном месте в яти сделать себе удобнее жизнь, то ты делаешь отдельную [View][View], которая будет работать с твоими данными и делать трансформацию для яти. Большинство переиспользуемых [View][View] принимают в конструкторе [Модели][Models], чтобы потом удобно трансформировать их для яти.


## Как начать обрабатывать новый урл?

1. Создать новую страницу: `make pages/majestic/response/generator`.
   Это создаст в папку `pages/majestic/response/generator` и в ней
   * `GeneratorPage.js` — Страницу, которая будет получать контроль над запросом.
   * `GeneratorLayout.js` — Лэйаут страницы, который знает где искать скомпилированный шаблон.
   * `generator.yate` — Шаблон
   * `generator.js` — Клиентские скрипты
   * `generator.styl` — Стили
   
2. В [рутере][Router] определить урл, по которому будет отвечать страница:
   ```javascript
   .map('/generate/awesomeness', require('./pages/majestic/response/generator/GeneratorPage'))
   ```



[Router]: https://github.yandex-team.ru/passport-frontend/oauth/blob/master/router.js
[Page]: https://github.yandex-team.ru/passport-frontend/oauth/blob/master/pages/AbstractPage.js
[Controller]: https://github.yandex-team.ru/passport-frontend/oauth/blob/master/controller/Controller.js 
[Api]: https://github.yandex-team.ru/passport-frontend/lib-apis/blob/master/OAuth/index.js
[Layout]: https://github.yandex-team.ru/passport-frontend/oauth/blob/master/blocks/layout/LayoutView.js
[CompositeView]: https://github.yandex-team.ru/passport-frontend/oauth/blob/master/lib/views/CompositeView.js
[View]: https://github.yandex-team.ru/passport-frontend/oauth/blob/master/lib/views/View.js
[Models]: https://github.yandex-team.ru/passport-frontend/oauth/tree/master/lib/models
[ClientModel]: https://github.yandex-team.ru/passport-frontend/oauth/blob/master/lib/models/Client.js


## Как поднять

Выставить порт в консоли (находясь в корне проекта):
```
npm config set yandex-oauth-frontend:port <your port>
```

Завести конфиг энджинкса (`sudo vim /etc/nginx/sites-available/yandex-oauth-frontend-<your login>`)
```
server {
        listen [::]:80;
        server_name ~^<your login>\.oauth\-dev\-trusty.(?:yandex|yandex\-team)\.(ru|com|com\.tr)$;

        location / {
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Real-Scheme $scheme;
                proxy_pass http://localhost:<your port>;
        }
}

server {
        listen [::]:443;
        server_name ~^<your login>.oauth\-dev\-trusty.(?:yandex|yandex\-team)\.(ru|com|com\.tr)$;

        ssl on;
        ssl_certificate certs/oauth.crt;
        ssl_certificate_key certs/oauth.key;
        ssl_prefer_server_ciphers on;
        ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;
        ssl_ciphers kEECDH+AES128:kEECDH:kEDH:-3DES:kEDH+3DES:kRSA+AES128:AES128-SHA:DES-CBC3-SHA:!RC4:!aNULL:!eNULL:!MD5:!EXPORT:!LOW:!SEED:!CAMELLIA:!IDEA:!PSK:!SRP:!SSLv2;
        ssl_session_cache shared:SSL:32m;
        ssl_session_timeout 5m;

        location / {
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Real-Scheme $scheme;
                proxy_pass http://localhost:<your port>;
        }
}
```

Подгрузить конфиг
```
sudo ln -s /etc/nginx/sites-available/yandex-oauth-frontend-<your login> /etc/nginx/sites-enabled/yandex-oauth-frontend-<your login> 
sudo /etc/init.d/nginx restart
```

Запустить (находясь в корне проекта)
```
make && npm start
```
