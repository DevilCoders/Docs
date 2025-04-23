# Серверный код

Управление данными в серверной части осуществляется с помощью двух модулей: [controller](https://a.yandex-team.ru/arcadia/classifieds/nodejs/nodejs-nodules-controllers) и [resource](https://github.com/YandexClassifieds/nodejs-resource).

## Controller

Расположение: `<service>/app/controller/pages/`

Каждый контроллер отвечает за конкретную страницу: главная, листинг, страница объявления.

### Миксины

Расположение: `realty-core/app/controller/mixin/` и проектные `<service>/app/lib/controller/mixins/`

Своего рода hoc для контроллеров.

Основные:
- `call-resource` - добавляет в прототип контроллера метод `callResource`, который используется для получений данных из бекенда
- `provides` - реализует механизм дата-провайдеров (о них ниже)
- `user_auth` - дополняет контроллер данными пользователя, если он аутентифицирован
- `user_region_info` - дополняет контроллер информацией о текущем регионе из геобазы (выбранном или геолоцированном)

### Дата-провайдеры

Расположение: `realty-core/app/providers/` и проектные `<service>/app/providers/`

Механизм разрешения зависимостей при получении данных из различных источников (бекенды, API).

Пример декларации выглядит так:

    // search.js
    
    const { Page } = require('@vertis/nodules-controllers');
    const SearchReactPage = Page.create();

    SearchPage.dataProviderDecl('offers', [ 'user-region-info', 'user-auth' ], function(data) {
        const { regionInfo, auth } = this.user;

        return this.callResource('searcher.offers', { rgid: regionInfo.rgid, uid: auth.uid }, { isMandatory: true })
            .then(result => data.offers = result);
    });
    
Тут, в контроллере `SearchPage`, декларируется провайдер `offers`. Опция `isMandatory` указывает на то, что успешное исполнение этого ресурса обязательно, иначе будет страница не будет загружена.
Он зависит от провайдеров `user-region-info` и `user-auth`, то есть начнет выполняться только после успешного исполнения этих двух.
В свою очередь, другой провайдер может указать себе в зависимости этот. И так далее.

Если какой-то из провайдеров в цепочке завершится неудачно (ошибка, исключение, `isMandatory` в ресурсе) - зависимые от него провайдеры не будут исполнены.

Провайдеры, объявленные в одном контроллере, можно вызвать в другом, подключив первый и использовав метод `getProvider`

    // other.js
    
    const SearchPage = require('./search.js');
    
    OtherPage.dataProvider('offers', SearchPage.getProvider('offers'));

Сигнатура метода: `dataProvider(string name, string|string[] dependencies?, function callback?)`

Если callback задан (или получен через `getProvider` из другого контроллера) - провайдер будет исполнен с указанной в этом callback реализацией.

Если не задан - контроллер попробует найти задекларированный провайдер из родителя, в случае неудачи выкинет исключение.

Если вы создаете отдельный провайдер, то данные лучше положить в один ключ:

    // your-provider.js
    
    data.yourPrivider = {
        key1: {}, 
        key2: {}
    }

Это будет полезно, если нужно будет воспользоваться гейтом react-page. При запросе данных, исходя из списка провайдеров, он мапит название задекларированного провайдера в ключ, который находится в объекте data.
https://a.yandex-team.ru/arcadia/classifieds/realty-frontend/realty-www/app/controller/pages/page.js?rev=r9618840#L468

### Гейты

Расположение: `<service>/app/controller/gates/`

Обработчик клиентских ajax запросов.

Пример декларации:

    // offer.js
    
    const { Gate } = require('@vertis/nodules-controllers');
    const GateOffer = Gate.create();
    
    GateOffer
        .action({
            name: 'get',
            schema: {
                required: [ 'id' ],
                properties: {
                    id: {
                        type: 'string',
                        minLength: '1'
                    }
                }
            },
            fn() {
                return this.callResource('offers.getById', this.getParams())
                    .then(offer => ({ id: offer.id, title: offer.title }));
            }
        })
        
В гейте `GateOffer` объявляется метод `get`, доступный по урлу `/gate/offer/get`.

Свойство `schema` описывает валидацию схемы данных в формате tv4, fn() - обработка запроса и что вернет гейт.

## Resource

Расположение: `realty-core/app/resource/`

Хелпер для работы с внешними (и внутренними) источниками, включая управление кешированием, обработки входных и выходных данных.

Есть два варианта

    const Resource = require('resource');
    const TipsResource = Resource.create();
    
    TipsResource.cfg = {
        ...config.get('tips.servant'), // конфиг из датасорсов / переменных окружения: protocol, host, port...
        agent: { name: 'tips', maxSockets: 1040 }, // настройка пула соединений
        cache: {
            get: { keyTTL: 1000 * 60 * 5 } // время жизни кеша для определенной ручки
        }
    };
    
    TipsResource
        .method('get', {
            prepare(opts) {
                const { uid, ...options } = opts;
    
                return this.prepareRequestOpts(`/tips/${uid}`, options);
            },
            process(res) {
                return res;
            }
        })
        .method('put', {
            prepare(opts) {
                const { uid, ...options } = opts;
    
                return this.prepareRequestOpts(`/tips/${uid}`, options);
            },
            process(res) {
                return { success: res.status === 'OK' };
            }
        });
     
Задаются методы `get` и `put`, которые, будут доступны в контроллере с названиями `tips.get` и `tips.put`.

Методы `prepare` и `process` описывают обработку параметров запрос и данные ответа соответственно.

Для обработки параметров запроса можно переопределить метод `prepareRequestOpts`. Параметры запроса прокидываются в [asker](https://github.com/nodules/asker) (обертка над http).

Если у ресурса всего один action, можно просто переопределить метода `prepareRequestOpts` и `processResultData`, однако, это выглядит менее лаконично.

Для непростых API есть возможность вмешаться в процесс обработки ответа:

через переопределение обработки мета-информации ответа `processResponseMeta`

    TipsResource.prototype.processResponseMeta = function(response) {
        this._statusCode = response.statusCode; // тут http-статус ответа
        this._headers = responce.headers; // тут лежат заголовки
    
        return Resource.prototype.processResponseMeta.call(this, response);
    };

и сырых данных `processRawResult`

    TipsResource.prototype.processRawResult = function(rawData) {
        this.rawResponse = rawData; // Buffer с ответом
    
        return Resource.prototype.processRawResult.call(this, rawData);
    };
