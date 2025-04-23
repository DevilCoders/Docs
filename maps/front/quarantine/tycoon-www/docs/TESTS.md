## Тесты

### Доступы
Если не работают тесты - запросить доступ к гриду https://wiki.yandex-team.ru/search-interfaces/infra/infratest/duty/Tunneler/#vydachadostupov. Если не спасло – писать на infraduty@

### Локальный запуск тестов
1. Запросить роль https://nda.ya.ru/t/tCR0D_po5FLHVH
1. Сделать экспорт в локальных переменных `export HERMIONE_OAUTH_TOKEN=<token>`, где token можно получить по ссылке https://nda.ya.ru/t/oS7IIVYz5FLKkR

### Стабы данных для ручек
Когда делаем запрос на сервер (метод request) нужно указать параметр stub:

``` js
const path = require('path');

request(req, `/example/handler/`, {
    method: 'GET',
    stub: path.join('{PATH}', 'STUB_NAME.get')
});
```

#### Расшифровка параметров:
  * `'{PATH}'` – имя папки, в которой будет лежать json со стабом (обычно определено как STUB_PREFIX на уровне модуля в backends/)
  * `STUB_NAME` - имя файла со стабом.
  * `get` – желательно указывать http метод, которым вызывается ручка (post, delete...)

При запуске в режиме чтения стабов `/example/handler/` будет отдавать файл `data-stubs/{PATH}/STUB_NAME.get.json`

#### Запустить сервер в режиме чтения стабов
В таком случае вместо реальных запросов будут браться данные из \*.json файлов в data-stubs/

`USE_STUB=1 npm start` либо npm `run start-stub`

### hermione

1. Запускаем в отдельной вкладке сервер со стабами `npm run ci:hermione:server`
2. В другой вкладке запускаем тесты командой `npm run test-hermione`
3. Для отладки можно делать в тестах скриншоты командой `.saveScreenshot('111.png')`
4. Удобное снятие скриншотов - `hermione gui` рядом с запущенным сервером

Если нужно запустить тест со снянием видео, то в строке запуска добавляем `--debug`.

Для разработки тестов можно так же использовать сокращенный вариант:
- Запустить без ретраев только в хроме, опционально указав путь до теста `hermione --retry 0 -b chrome [FILE]`

#### Работа со скриншотами
Если нужно добавить скриншоты – запускаем `hermione --update-refs`

##### Детали
[Пост в этушке про assertView()](https://clubs.at.yandex-team.ru/search-interfaces-serp/1635)
[Серповая дока. Куча подробностей](https://wiki.yandex-team.ru/search-interfaces/testing/hermione/#construct-blocks)

##### Запуск отчета гермионы из CI локально
Бывает удобно для переснятия скриншотов

```
ya download sbr:<id> --output=./reports/hermione-report --overwrite
chmod 666 ./reports/hermione-report/databaseUrls.json && \
chmod 666 ./reports/hermione-report/data.js && \
chmod 666 ./reports/hermione-report/sqlite.db

npm run test-hermione -- gui --retry=0
```

### Тесты на ручки
Тесты на ручки вызывают ручку, и проверяют в ней наличие необходимых параметров. Избыточные поля игнорируются.
Тесты работают на стабах из data-stubs. Сами тесты лежат в [server/test/](/server/test/)

Проверяющий код лежит в [server/test/test-environment.js](/server/test/test-environment.js)

Для того, чтобы посмотреть, что отдает ручка нужно:
1. Запустить `RENDER=json npm run start-stub`
2. Открыть ссылку, например http://localhost:8082/1/edit/reviews/

#### Запуск тестов
`npm run test-unit-server`

#### Написание тестов [Deprecated]
Устаревший способ разработки серверных тестов. Документация может быть использована для починки падающих существующих тестов.

**N.B.** Новые тесты следует разрабатывать с использованием схем (см. server/test/controllers/tests.js и server/test/schemes)

``` js
const env = require('./test-environment');

env.urlTester({
    testName: 'Содержательное и лаконичное имя теста',
    testCases: [
        {
            url: '/handler', // Ручка, которую вызываем в режиме отдачи json,
            body: env.genResponseBody({ // Указываем в объекте поля, которые обязательно должны быть в результат (Помимо стандартных, типа `user`, `env`...)
                view: 'page-blabla',
                navigation: true
            })
        }
    ]
});
```

#### Для получения моков данных
1. Указываем в спеке вместо готового мока данных строку указывающую на источник этих данных (см. пример). При построении спеков указанный URL будет запрошен у сервера (стартует автоматически на генерацию спеков) и произведена замена исходной строки на полученные данные. Запросить можно и `json`, и `bemjson`. Для получения только части необходимых данных можно использовать параметр запроса `jspath` c [jspath](https://github.com/dfilatov/jspath#usage) к необходимой части данных, в формате `__LOADMOCK:${URL}__`. Например, тут находится блок `badges`
```js
const json = JSON.parse(
  '___LOADMOCK:/cards/89521921?bemjson=1&jspath=..content{.block==="badges"}[0]___');
```
будет заменено при сборке на
```js
const json = JSON.parse(
    '{"block":"badges","mods":{"type":"list","theme":"islands","size":"s"}...'
);
```
1. `N.B.` Строку с параметром запроса (`__LOADMOCK:${URL}__`) разрывать/переносить нельзя :)
1. Для запроса данных можно использовать и `POST` запросы, для этого вместо простой строки - урла запроса `${URL}` в `__LOADMOCK:${URL}__` нужно указать *валидный* `JSON` с параметрами запроса (`url`, `method`, `body`). Например:
```js
const bemjson = JSON.parse(
    '___LOADMOCK:{"body":{"id":123},"url":"/api/blacklist-modal/?bemjson&jspath=..{.block==\"blacklist-edit\"%26%26.elem==\"content\"}[0]"}___'
);
```
1. Если `body` указан, то по умолчанию `method: 'POST', headers: { content-type: application/json }`
1. Кавычки в `jspath` приходится экранировать

#### Просмотр упавших тестов в Trendbox
https://wiki.yandex-team.ru/search-interfaces/infra/trendbox/Kak-posmotret-chto-upalo-poka-net-UI/
