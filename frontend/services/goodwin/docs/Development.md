# Архитектура

## Runtime

Приложение работает под [Report Renderer](https://wiki.yandex-team.ru/search-interfaces/infra/report-renderer/) и представляет из себя, собственно, шаблоны для Report Renderer. Точка входа в шаблон — [src/entries/server/server.ts](../src/entries/server/server.ts)

Результат шаблонизации формируется на основе поисковых данных, по запросу пользователя. В приложение приходят данные через `wizplaces`, `searchdata.docs` и `searchdata.doc_right`, которые обрабатываются через [taburet](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/taburet). Taburet на основе `type` и `subtype`, указанных в данных, выбирает адаптер, который в свою очередь сериализуется в формат [Talkien](https://wiki.yandex-team.ru/users/the0/alice/json-based-interaction/) с помощью [Базового класса](./BaseClasses.md)

Кроме вызова подходящих адаптеров, происходит формирование контекста запроса, который используется адаптерами. Контекст содержит информацию о запросе: текст запроса, reqid, данные о пользователе и т.д. Но кроме этого Megamind присылает специальный заголовок `x-yandex-alice-meta-info` в формате protobuf с дополнительными данными:

`requesttype` - источник запроса ("Goodwin" или "Megamind")
`clientinfo` - информация об устройстве (поверхность, язык, время запроса пользователя и т.д.)

В коде с этими данными можно работать через свойство `deviceInfo` у контекста.

## Adapter

Адаптер трансформирует данные от бекенда к формату [Talkien](https://wiki.yandex-team.ru/users/the0/alice/json-based-interaction/), необходимому для Megamind. Чтобы добавить новый адаптер

1. Создайте в папке [features](../src/features/) папку и файл для своего адаптера, конвенция на имена файлов такая: `features/MyAdapter/MyAdapter.server.ts`
2. Напишите код адаптера — сниппет готовит метод `transform`, опишите для адаптера тип входящего сниппета. Метод `transform` должен возвращать объект для Алисы типа [IAliceGoodwinDoc](../src/typings/goodwin.d.ts#L1)
3. Сформируйте ответ с помощью [Базового класса
4. Зарегистрируйте адаптер в реестре [features/.registry/common](../src/features/.registry/common.ts) — в реестре хранится соответствие пары `type`/`subtype` сниппета и класса адаптера, которым нужно обработать этот сниппет

## Базовый класс

Ответ каждого сценария, формируется базовым классом [`AliceDocResponse`](../src/lib/response/index.ts), который умеет:

* Добавить голосовой ответ
* Добавить текстовый ответ, включая дивные карточки
* Установить данные для аналитики
* Добавить саджесты с запуском `action` для ПП
* Добавить набор `action` с срабатыванием на опредленные фразы или грамматики
* Установить "семантический фрейм", для помощи Megamind'у в выборе сценария
* Указать Алисе, что нужно продолжать слушать пользователя

### Пример использования

    const response = new AliceDocResponse(
        'TestFeatureType', // или объект полями 'type' и 'subtype'
        'Голосовой ответ',
        'Текстовый ответ', // также можно передать дивные карточки
        {} // дополнительные параметры
    );

    return response.serialize();

### Аналитика

Каждый сценарий содержит информацию для аналитики − `analytics_info`, в котором есть два поля `product_scenio_name` и `intent`

#### product_scenario_name
Основной параметр группировки сценариев для аналитики, используется в ab-метриках и [дашбордах](https://nda.ya.ru/t/hQmMaORf3Vyqfg). Допустимы латинские буквы в нижнем регистре и знак нижнего подчеркивания '`_`'. На классификацию в Мупфьштв это поле не влияет.

Примеры: `find_poi`, `covid`.

Базовый класс, по умолчанию создает его со значениеv типа сценария, например, `{ analyticsinfo: { product_scenario_name: <type> } }`. Рекомендуется указать его вручную

    response.setProductScenarioName('scenario_name')

#### intent
Позволяет дробить сценарии. Уточняет пользовательский сценарий для `product_scenario_name`.
Например, по интенту строится график dau − https://dash.yandex-team.ru/bde47pj1yezm7?tab=jNN.

Пример: `goodwin.find_poi.1org` и `goodwin.find_poi.orgmn`.

Базовый класс, по умолчанию создает его со значение типа сценария, например, `{ analyticsinfo: { intent: <type>[_<subtype>] } }`. Рекомендуется указать его вручную

    response.setAnalyticsInfo('scenario_name', 'scenario_intent')

Если не указать intent при вызове setAnalyticsInfo, то выставится в значение 'scenario_name'

### Сохранение состояния

Между запросами можно сохранять данные. Для этого можно воспользоваться методом `setState`

    response.setState({ field: ['value1', 'value2'] });

Далее эти данные, можно использовать в адаптере

    JSON.parse(this.context.request.body).goodwin.state

### Текстовый ответ

Текстовый ответ можно задать не только при создании инстанса `AliceDocResponse`, для этого предусмотрены методы `setText`, `setCards` и `addCard`. Последние две позволяют дать ответ в формате дивных карточек.

### Actions

В данныом разделе рассматриваются только серверные `Action`, которые позволяют отреагировать на действие пользователя, например, открыть url, выполнить дозапрос, отправить Пуш и запустить внешний сценарий

* `OpenUriAction`

Позволяет открыть страницу в ПП, пример использования:

    docResponse.addAction(new OpenUriAction(
        'more',
        url,
        ['перейди', 'подробнее', 'покажи', 'расскажи', 'карта', 'страница', 'перейти к карте', 'покажи карту'],
    ));

* `CallbackAction`

Позволяет сделть дозапрос, чтобы отдать пользователю новый ответ, пример использования:

    docResponse.addAction(new CallbackAction(
        'about',
        url,
        ['Что такое коронавирус', 'что это', 'расскажи про коронавирус', 'давай про коронавирус', 'что это за вирус', 'про коронавирус'],,
    ));

* PushAction

Позволяет отправить Пуш пользователю, пример использования

    new PushAction(
        'push',
        baseUrl,
        [
            'заказать',
            'заказать исполнителя',
            'вызвать',
            'показать',
            'найти',
            'помоги',
            'помоги вызвать',
            'цена',
        ],
        new Push(
            passportUserId,
            'alice_goodwin_ydo_link',
            'Яндекс.Услуги',
            this.snippet.workers_in_geo + chooseOne<string>(...endsOfPushText),
            this.snippet.path[this.snippet.path.length - 1].url,
        ),
    )

* ExternalFrameAction

Позволяет запустить внешний сценарий, пример использования

    docResponse.addAction(new ExternalFrameAction(
        'goodwin.music',
        'personal_assistant.scenarios.music_play',
        ['окей'],
        [{
            name: 'search_text',
            type: 'string',
            value: `${groupName} песня ${track.title}`,
            accepted_types: ['string'],
        }]
    ));

### Suggests

Саджесты доступны только в ПП, они запускают указанный для саджеста `action` при нажатии на него. Пример использования в сценарии

    docResponse.setSuggests([
        { action_id: 'about', title: 'Что такое коронавирус' },
        { action_id: 'statistics', title: 'Статисстика по России' },
    ])

Action'ы `about` и `statistics` должны быть ранее добавлены в сценарий с помощью `addAction`

## Тесты

### E2E тесты

#### Запуск тестов

* `npm run e2e:local` - команда для запуска тестов на локальных шаблонах
* `npm run e2e:production` - команда для запуска тестов на шаблонах продакшена

На каждую фичу должен быть написан тест, который распологается рядом с кодом фичи.

    /src/features/Covid/Covid.server.ts - код фичи
    /src/features/Covid/Covid.test/Covid.e2e.js - e2e-тесты фичи

#### Пример теста

В контексте каждого теста доступен объект `client`, который позволяет делать полноценные запросы к Алисе. Например:

    specs('Колдунщик коронавируса', () => {
        it('Дефолтный', async function() {
            const response = await this.client.request('корон');

            this.asserts.yaCheckAnalyticsInfo(response, { product_scenario_name: 'covid', intent: 'covid_base' });
            this.asserts.yaCheckVoiceInclude(response, 'У меня есть много информации про коронавирус');
            this.asserts.yaCheckTextInclude(response, 'У меня есть много информации про коронавирус');
    });

Вторым параметром в вызов `request` можно передать дополнительные параметры, например экспериментальные флаги.

    const response = await this.client.request('корон', {
        flags: {
            exp1: 'exp1_value',
            exp2: [],
        },
    });

#### Хелперы

* `yaCheckAnalyticsInfo` - проверка наличия данных для аналитики
* `yaCheckVoice` - проверка голосового ответа, третий параметр позволяет проверить вхождения текста в ответе
* `yaCheckText` - проверка текстового ответа, третий параметр позволяет проверить вхождения текста в ответе

#### Поверхность

По умолчанию в качестве поверхности для теста используется "мини-станция", но есть возможность изменить поверхность, например, на ПП.

    specs('Колдунщик коронавируса (SEARCHAPP)', SURFACES.SEARCHAPP, () => {
        ...
    })

Все тесты в данном `specs` будут выполнены для ПП. Полный список, доступных в тестах поверхностей, находится [здесь](../test/e2e/lib/uniproxy/surfaces.js)