
# Кабинет дилера

## Структура кабинета
Кабинет состоит из 4 различных проектов для разных типов пользователей:
* cabinet.auto.ru - кабинет для дилера
* agency.auto.ru - агенство
* company.auto.ru - группа компаний
* manager.auto.ru - менеджер (CRM)

Вместо auto.ru можно подставить тестовый домен (https://agency.test.avto.ru) или дев-домен (пример: https://cabinet.frontend.stormtrooper.dev.avto.ru).

## Где брать тестовых пользователей для разработки и отладки?

Можно использовать `demo@auto.ru / autoru`, (тип клиента - дилер, заходить на cabinet.*)

Нужно залогиниться под менеджером (пример: avgribanov@yandex-team.ru), зайти на https://manager.test.avto.ru, нажать в шапке Клиенты / Агенты / Группа компаний, выбрать подходящего клиента в списке и кликнуть по нему. В информации о пользователе будет его email - его можно использовать для входа в кабинет (пароль стандартный - `autoru`).

## Пополнение кошелька для различный типов клиентов
В кабинете могут работать различные типы пользователей, для них есть разные комбинации возможностей пополнения кошелька

| Тип клиента  | Выставление счета  | Оплата картой |
|:------------- |:---------------:| :-------------:|
| **Прямой клиент**     | + |     + |
| Прямой клиент под менеджером | +        |     - |
| Прямой клиент ГК      | +       |         +   |
| **Агентский клиент** | -        |     - |
| Агентский клиент под агенством | +        |     - |
| Агентский клиент под менеджером | +        |     - |
| Агентский клиент под ГК | -        |     - |

### Откуда брать
Возможные варианты оплаты приходят в ручке publicAPI [GET /dealer/account](http://autoru-api-server-int.vrts-slb.test.vertis.yandex.net/swagger/?url=/api-docs#!/dealer/getDealerAccount)

### Когда какой способ доступен:
- card_payment - дилер не принадлежит агентству и роль пользователя который делает запрос = клиенту или группе компаний
- invoice - дилер не принадлежит агентству и роль пользователя который делает запрос = клиенту или группе компаний или менеджеру
- invoice_request - всегда доступна агентству или менеджеру иначе доступна если клиент не принадлежит агентству

### Сами ручки оплаты (кабинетное API)
1) для invoice - [POST /client/{client_id}/invoice](http://autoru-cabinet-api-01-sas.test.vertis.yandex.net:2030/swagger.html#!/invoice/postInvoice)
2) для invoice_request - [POST /client/{client_id}/invoice/request](http://autoru-cabinet-api-01-sas.test.vertis.yandex.net:2030/swagger.html#!/invoice/postInvoiceRequest)
3) для оплаты картой - [POST /client/{client_id}/payrequest](http://autoru-cabinet-api-01-sas.test.vertis.yandex.net:2030/swagger.html#!/invoice/postPayRequest)

[Документация с перечислением ручек и краткой информацией](https://wiki.yandex-team.ru/users/avgribanov/frontend-cabinet)

## Добавление общих ручек

Общие ручки для кабинетов лежат в `frontend/auto-core/lib/api-methods/apiCabinetCommon.js`.
В некоторых ручках resource указан как null, это значит, что ручка используется с одинаковыми параметрами в обоих кабинетах. Такую ручку необходимо расширить, указав нужный resource и в случае агентского кабинета необходимо также расширить параметры ручки, передав client_id.

Пример общей ручки:

    getSomeData: {
        resource: null,
        path: 'some/path',
        params: {
            id: null,
            status: null
        }
    }

## Ручки дилерского кабинета

Ручки для дилерского кабинета лежат в `frontend/auto-core/lib/api-methods/apiCabinet.js`.
Если используется общая ручка, то ее необходимо объявлять следующим образом:

    getSomeData: extendCommonHandler('getSomeData')

Функция extendCommonHandler устанавливает `resource` в значение `api-cabinet` и добавляет к параметрам `client_id`.

## Как добавить новую страницу

### Создать контроллер страницы

Контроллеры лежат в папке `app/controller/pages`.
Можно взять `index.js` и скопировать в новый файл.
Все, что нужно в нем поправить (как правило), это вот этот кусок:

    const core = require('auto-core');

    module.exports = core.controllers.create([
        'search',
        'testdriveList',
        'newsList',
    ]);

В массиве лежат имена методов API, которые нужны для построения этой страницы.
Это не те имена, которые собственно в документации API приведены (например, `news.news.getList`),
а короткие алиасы, описанные в файле https://github.yandex-team.ru/autoru-www/auto-core/blob/master/lib/api-methods/index.js.
Описания этих методов выглядит примерно так:

    newsItem: {
        method: 'news.news.get',
        params: {
            news_id: null
        }
    },

Здесь `newsItem` — это короткое имя для метода API `news.news.get`.
Оно используется для описания контроллеров (см. выше).

Кроме того, в результирующем json-дереве ответ этого метода будет в `data['newsItem']`.
Есть возможность поменять это параметром `id`:

    newsItem: {
        id: 'news',
        method: 'news.news.get',
        ...

В этом случае ответ метода будет в `data['news']`.

Если метод не принимает параметров, то `params` не нужны вовсе.
В противном случае, все параметры, которые принимает метод, нужно описать явно:

    params: {
        category_id: 15,
        sale_id: null
    }

Здесь любое значение, кроме `null`, означает дефолтное значение параметра.
`null` — просто параметр, без дефолтного значения.

Есть еще более сложные варианты:

    params: {
        ...
        sale_id: function (query) {
            var sale_id = query['sale_id'];
            var sale_hash = query['sale_hash'];

            return (sale_hash) ? sale_id + '-' + sale_hash : sale_id;
        }
    }

В этом случае значение параметры `sale_id` вычисляется динамически. В функцию приходят все параметры запроса (из урла страницы).

Ну и последний вариант:

    params: function (query) {
        return {
            sale_id: query.sale_id
        };
    }

В этом варианте вообще все параметры вычисляются динамически.

### priv.js

Файлы лежат в `blocks/page`.

  * Добавить файл `page/_type/page_type_<NAME>.priv.js` (`<NAME>` — это имя контроллера в роутере).

  * Добавить в файл `page/page.deps.js` вот сюда

        mods: {
            type: [
                'index',
                'sale',
                ...
            ]

    имя этой новой страницы.

  * Сделать `make privs`.

После чего по тому же урлу, но уже с параметром `__bemjson` (`__raw` нужно убрать из урла) должен быть виден BEMJSON,
который получился после применения priv'а. А без всех этих параметров собственно верстка.



## Code Style

### JS

Используется [ESlint](http://eslint.org/) и EditorConfig.

#### Настройка IDE

##### JetBrains с js (WebStorm, PhpStorm, IDEA и др.)

Включить ESLint:

    Preferences → Languages & Frameworks → JavaScript → Code Quality Tools → ESLint.

Указать путь к ESLint пакету:

    /<project_root>/node_modules/eslint

Путь к конфигурационному файлу:

    /<project_root>/.eslintrc

EditorConfig должен сработать автоматически по-умолчанию. Если же нет, тогда включите EditorConfig plugin и перезапустите редактор.

##### Sublime Text

Установите пакет:

    $ npm install -g eslint

Установите плагины:

* SublimeLinter
* SublimeLinter-contrib-eslint
* EditorConfig

### Stylus

https://beta.wiki.yandex-team.ru/autoru-dev/frontend/stylus/
