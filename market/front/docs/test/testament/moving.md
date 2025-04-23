# Перенос тестов с hermione на testament

Данный документ представляет из себя гайд по переводу гермионовых тестовых на testament. ((https://github.yandex-team.ru/market/testament Testament)) - библиотека, предназначенная для тестирования apiary-виджетов с использованием jest и kadavr.

> Данная статься за авторством [Никиты Мигунова](https://staff.yandex-team.ru/creazero) является отличным руководством по переносу тестов. Оригинал тут: https://wiki.yandex-team.ru/users/creazero/perevod-testov-hermione-na-testament/ Сататья немного сокращена/изменена.

# Зачем переносить
- Сделать тесты маркета быстрее
- Сделать тесты маркета стабильнее
- Единый подход к тестированию виджетов
- Выравнивание пирамиды тестирования (у нас много e2e и мало интеграционных/юнит тестов)

# Общий подход
При переносе теста с гермионы на тестамент, нужно просмотреть тест с точки зрения виджетов, которые используются в этом тесте. Если тест на гермионе тестирует только один виджет (Например ДО), то переносим "как есть", немного (много) меняя код теста под требования тестамент. Если же тест гермиона тестирует несколько виджетов на странице(страницах), то придется распиливать такой тест гермиона на составляющее, так как на тестаменте мы тестируем виджеты и только виджеты. Какие-то части которые "хорошо" тестируются тестаментом, нужно переносить в тестамент, а какие-то, возможно, оставить в гермиона тесте.

## Определение подходит ли тесты для переноса на testament
Идеально для переноса подходят тесты, в которых все проверки проходят в одном виджете без смены страниц и открытия новых вкладок. Если нужно протестировать какой-нибудь сценарий взаимодействия нескольких виджетов (даже на одной странице), то лучше использовать гермиону, чтобы не затаскивать в пайплайн гитхаба огромные деревья виджетов.

### Хороший для переноса тест
```js
{
    'Неавторизованный пользователь.': {
        async beforeEach() {
            return this.browser.yaOpenPage(this.params.pageId);
        },
        'Текст отображается корректно': makeCase({
            async test() {
                await this.zeroState.title.getText()
                    .should.eventually
                    .to.be.equal(ZERO_STATE_UNAUTHORIZED_TITLE);

                await this.zeroState.text.getText()
                    .should.eventually
                    .to.be.equal(ZERO_STATE_UNAUTHORIZED_TEXT);

                await this.zeroState.button.getText()
                    .should.eventually
                    .to.be.equal('Войти');
            },
        }),
    },
}
```

### Неподходящий для переноса тест
```js
{
    'При клике': {
        'должна открываться КМ': makeCase({
            async test() {
                const currentTabId = await this.browser.allure.runStep(
                    'Получаем идентификатор текущей вкладки',
                    () => this.browser.getCurrentTabId()
                );
                await this.snippet.click();
                const newTabId = await this.browser.yaWaitForNewTab({
                    startTabIds: [currentTabId],
                    timeout: 2000,
                });

                await this.browser.allure.runStep(
                    'Переключаем вкладку на только что открытую вкладку карточки продукта',
                    () => this.browser.switchTab(newTabId)
                );

                const productUrl = await this.browser.getUrl();

                await this.browser.close();
                await this.browser.allure.runStep(
                    'Переключаем вкладку на начальную',
                    () => this.browser.switchTab(currentTabId)
                );

                return this.browser.allure.runStep(
                    'Проверяем, что url открытой вкладки соответствовал продуктовому url',
                    () => Promise.resolve(productUrl)
                        .should
                        .eventually
                        .be
                        .link({
                            pathname: `/product--${productKettle.slug}/${productKettle.id}`,
                        }, {
                            skipProtocol: true,
                            skipHostname: true,
                        })
                );
            },
        }),
    },
},
```

### Пример перевода теста
Ниже будет представлен примерный процесс перевода теста с гермионы на тестамент.


```js
export default makeSuite('Ранее купленные.', {
    environment: 'kadavr',
    params: {
        pageId: 'Открываемая страница',
    },
    defaultParams: {
        pageId: 'market:purchased',
    },
    story: {
        'Пустая история': {
            async beforeEach() {
                this.setPageObjects({
                    zeroState: () => this.createPageObject(ZeroStateCard),
                });
            },

        'Неавторизованный пользователь.': {
            async beforeEach() {
                return this.browser.yaOpenPage(this.params.pageId);
            },

            'Текст отображается корректно': makeCase({
                async test() {
                    await this.zeroState.title.getText()
                        .should
                        .eventually
                        .to
                        .be
                        .equal(ZERO_STATE_UNAUTHORIZED_TITLE);

                    await this.zeroState.text.getText()
                        .should
                        .eventually
                        .to
                        .be
                        .equal(ZERO_STATE_UNAUTHORIZED_TEXT);

                    await this.zeroState.button.getText()
                        .should
                        .eventually
                        .to
                        .be
                        .equal('Войти');
                },
            }),

            'Клик по кнопке переводит на страницу авторизации': makeCase({
                async test() {
                    await this.zeroState.clickButton();

                    return this.browser.yaParseUrl()
                        .should
                        .eventually
                        .be
                        .link({
                            hostname: 'passport-rc.yandex.ru',
                            pathname: '/auth',
                        }, {
                            skipProtocol: true,
                        });
                },
            }),
        },

        'Авторизованный пользователь.': {
            async beforeEach() {
                return this.browser.yaProfile('pan-topinambur', this.params.pageId);
            },

            'Текст отображается корректно': makeCase({
                async test() {
                    await this.zeroState.title.getText()
                        .should
                        .eventually
                        .to
                        .be
                        .equal(ZERO_STATE_AUTHORIZED_TITLE);

                    await this.zeroState.text.getText()
                        .should
                        .eventually
                        .to
                        .be
                        .equal(ZERO_STATE_AUTHORIZED_TEXT);

                    await this.zeroState.button.getText()
                        .should
                        .eventually
                        .to
                        .be
                        .equal('За покупками');
                },
            }),

            'Клик по кнопке переводит на главную страницу': makeCase({
                async test() {
                    await this.zeroState.clickButton();

                    const currentUrl = await this.browser.getUrl();
                    const expectedUrl = await this.browser.yaBuildURL('market:index');

                    return this.expect(currentUrl)
                        .to
                        .be
                        .link(expectedUrl, {
                            skipProtocol: true,
                            skipHostname: true,
                        });
                },
            }),
        },
      },

      'Пользователь с купленными товарами': {
        'Список ранее купленных': {
          'Сниппет продута': {
            async beforeEach() {
              this.setPageObjects({
                  snippet: () => this.createPageObject(SearchProductTile),
                  wishlistTumbler: () => this.createPageObject(WishlistTumbler),
                  compareTumbler: () => this.createPageObject(CompareTumbler),
                  dealsTerms: () => this.createPageObject(DealsTerms),
              });

              await this.browser.setState(
                  'Checkouter',
                  {
                      collections: {
                          order: {
                              [ORDER_ID]: ORDER,
                          },
                      },
                  }
              );
              await this.browser.setState(
                  'report',
                  mergeState([
                    createProduct(productKettle, productKettle.id),
                    createOfferForProduct({
                        ...offerKettle,
                        promos: [
                            {
                                type: 'blue-cashback',
                                key: 'JwguUZO8-HIaOJ1J4_k0_Q',
                                description: 'Кэшбэк на все',
                                shopPromoId: '3vDxyRpFM8ycDVJiunVGRA',
                                startDate: '2020-09-14T21:00:00Z',
                                endDate: '2024-12-30T21:00:00Z',
                                share: 0.05,
                                version: 1,
                                priority: 199,
                                value: 207,
                            },
                        ],
                    }, productKettle.id, offerKettle.wareId),
                  ])
              );

              return this.browser.yaProfile('pan-topinambur', 'touch:purchased');
            },

            'по умолчанию': {
              'должен содержать кнопку добавления в избранное': makeCase({
                async test() {
                  const isExists = this.wishlistTumbler.isExisting();

                  return this.expect(isExists)
                        .to.be.equal(true, 'Кнопка присутствует на сниппете');
                },
              }),
            },
          },
        },
      },
    },
});
```
## Инициализация окружения
Перед написанием тестов на тестаменте требуется произвести инициализацию тестового окружения. Минимальный пример:
Шаблон [тут](examples/boilerplate.md)

## Тест без авторизации
Ниже представлен пример переноса простого теста (без авторизации и моков в кадавре)
Меняем в шаблоне следующее:

```js

const WIDGET_PATH = '@self/project/src/widgets/content/PurchasedGoods';

beforeAll(async () => {
    // ...минимальная инициализация

    // Вызов jestLayer для подмены роутера на обеих "сторонах" (сервер и клиент).
    // На текущий момент тестамент не подтягивает все роуты из конфига,
    // поэтому нужно писать такие моки.
    await jestLayer.runCode(() => {
        const {mockRouter} = require('@self/project/src/helpers/testament/mock');
        mockRouter({
            'external:yandex-passport': '//pass-test.yandex.ru',
            'market:index': '//market.yandex.ru',
        });
    }, []);
});

describe('Пустая история', () => {
    describe('Неавторизованный пользователь', () => {
        beforeEach(async () => {
            await makeContext();
        });

        it('Текст пустого состояния должен быть правильным', async () => {
            // Маунт виджета через apiaryLayer. Под капотом происходит стандартный
            // маунт из апиари.
            await apiaryLayer.mountWidget(WIDGET_PATH);

            expect(screen.getByRole('heading', {name: ZERO_STATE_UNAUTHORIZED_TITLE})).toBeInTheDocument();
            expect(screen.getByText(ZERO_STATE_UNAUTHORIZED_TEXT)).toBeInTheDocument();
            expect(screen.getByRole('button', {name: /войти/i})).toBeInTheDocument();
        });

        it('Ссылка с кнопкой должны вести на страницу авторизации', async () => {
            await apiaryLayer.mountWidget(WIDGET_PATH);

            const anchor = screen.getByRole('link', {name: /войти/i});
            expect(anchor).toHaveAttribute('href', 'http://pass-test.yandex.ru');
        });
    });
});
```

## Тест с авторизацией
Добавление авторизации в тест на тестаменте происходит максимально просто - достаточно просто добавить поле `isAuth` в контекст мандреля:
```js

-   async function makeContext() {
+   async function makeContext(user = {}) {
    const cookie = {kadavr_session_id: await kadavrLayer.getSessionId()};
    return mandrelLayer.initContext({
       request: {cookie},
+       user,
    });
}

// ... beforeAll, afterAll

    describe('Пустая история', () => {
        describe('Неавторизованный пользователь', () => {
        // ...
        });

+       describe('Авторизованный пользователь', () => {
+           beforeEach(async () => {
+                await makeContext({isAuth: true});
+           });
+
+            it('Текст пустого состояния должен быть правильным', async () => {
+               const {container} = await apiaryLayer.mountWidget(WIDGET_PATH);
+
+               expect(screen.getByRole('heading', {name: ZERO_STATE_AUTHORIZED_TITLE})).toBeInTheDocument();
+               expect(screen.getByText(ZERO_STATE_AUTHORIZED_TEXT)).toBeInTheDocument();
+               expect(screen.getByRole('button', {name: /за покупками/i})).toBeInTheDocument();
+           });
+
+           it('Ссылка с кнопкой должны вести на главную', async () => {
+                // ...
+           });
+       });
    });
```

### Добавление моков в кадавре
Работа с кадавром ничем не отличается от гермионы. Только вместо `this.browser.setState` нужно вызывать `kadavrLayer.setState`.

```js

describe('Список ранее купленных товаров', () => {
    describe('Сниппет продукта', () => {
        beforeEach(async () => {
            await kadavrLayer.setState(
                'Checkouter',
                {
                    collections: {
                        order: {
                            [ORDER_ID]: ORDER,
                        },
                    },
                }
            );

            await kadavrLayer.setState(
                'report',
                mergeState([
                  createProduct(productKettle, productKettle.id),
                  createOfferForProduct({
                    ...offerKettle,
                    promos: [
                      {
                        type: 'blue-cashback',
                        key: 'JwguUZO8-HIaOJ1J4_k0_Q',
                        description: 'Кэшбэк на все',
                        shopPromoId: '3vDxyRpFM8ycDVJiunVGRA',
                        startDate: '2020-09-14T21:00:00Z',
                        endDate: '2024-12-30T21:00:00Z',
                        share: 0.05,
                        version: 1,
                        priority: 199,
                        value: 207,
                      },
                    ],
                  }, productKettle.id, offerKettle.wareId),
                ])
            );

            await makeContext({isAuth: true});
        });

        it('должен содержать кнопку добавления в избранное', async () => {
            await apiaryLayer.mountWidget(WIDGET_PATH);
            // Даже если кнопка в виде иконки, она должна иметь доступное описание.
            expect(screen.getByRole('button', {name: /добавить в избранное/i})).toBeInTheDocument();
        });
    });
});
```

### Сценарии
Сценарии нужно дробить на фреймворко-независимые хелперы и гермионовые сценарии. Например, сценарий `prepareMultiCartState` нужно делить на хелпер, который делает все эти махинации со всеми нужными коллекциями, и на основной сценарий, который будет вызывать хелпер и делать уже нужный `this.browser.setState`.

## Особенности и известные проблемы

### Метаданные для тестов и Allure отчет
В тестаментовых тестах указывать метаинформацию (id, issue, etc) не требуется. После обсуждения с тестировщиками было решено, что т.к. тестаментовые тесты должны быть сильно стабильнее гермионовых тестов, то и метаинформация для поиска ответственных за тест тоже не потребуется.
В связи с этим для этих тестов Allure отчет использоваться не будет. На данный момент поддержка для степов (глобальная функция %%step%%) в тестаменте присутствует, но ни конфигурации в проекте, ни нормального прорастания этих степов в отчет нет. На текущий момент для тестов используется обычный отчет для юнит-тестов.

### Роутер
Как можно было заметить по примерам тестов, на данный момент в работе с роутером в тестах имеются некоторые неудобства. По умолчанию любой вызов `buildUrl` в тестируемом коде будет брать название пути (market:index), брать переданные параметры и просто склеивать эту красоту в единую строку.
Кажется, что особых проблем с поднятием полноценного роутера в тестаменте нет, но на данный момент это не реализовано.

### Кадавр
#### 1. Отсутствие походов в реальные бекенды
В Testament кадавр работает asLibrary, то есть без реальных походов в сеть.
Никакого похода в реальный бекенд нет - функция `_proxy` замокана таким образом, что при ее вызове просто бросается ошибка с сообщением "[Kadavr]: Can't find mock for ${this.originalHost}".

Простой пример - `resolveCompassInfo`. Если писать тест с сетевым кадавром, то будет достаточно замокать только путь `Cataloger.navigationTree`, и тест заработает. С локальным же кадавром оказывается, что есть еще путь `Cataloger.categoriesTree`, в случае отсутствия которого, кадавр просто бросает ошибку, которая потом превращается в вызов `_proxy`, который в свою очередь тоже бросает ошибку.

>Из-за этой особенности некоторые тесты, в которых замоканы не все нужные данные, могут потребовать дополнительной работы при переносе.

#### 2. Стена ошибок
Данная проблема выходит из особенности №1. При вызове `_proxy` бросается ошибка
про нереализованный путь и из-за этого в тестах появляются просто стены текста о том,
что есть какой-то путь по такому-то адресу, который сейчас нереализован
(хорошо еще, что пишется только хост, а то мы бы просто утопали в express warehouses).
Но на этом стена текста не заканчивается! Ведь сейчас тестамент бросает эту ошибку
в виде простой строки, которая потом попадает в MarketHttpTransport,
который пытается эту строку распарсить как JSON, не преуспевает в этом и
вываливает просто килотонну текста про это. Если просто заменить строку с
ошибкой на какой-нибудь JSON, то проблема с парсингом уходит, но появляются
TypeErrorы, которые возникают из-за отсутсвия какого-то обязательного поля в JSONе
с ошибкой.

Из-за этого поиск результатов теста (при запуске из терминала) требует какого-то
скроллинга, при чем при запуске бОльшего количества тестов,
скроллинга становится пропорцианально больше!

В теории проблема решается добавлением недостающих путей в кадавр
(с каким-нибудь дефолтными значениями), но тут мы переходим к 3 (мини-)проблеме.

#### 3. Кадавр очень долго релизится
Если для релиза сетевого кадавра вам достаточно просто найти любителя быстро
нажимать зеленые кнопки, замержить ПР, дождаться деплоя хотя бы тестинга кадавра и
начать использовать добавленные моки, то с локальным кадавром весь процесс
занимает сильно больше времени из-за того, что в начале нужно дождаться полного
прохода пайплайна релиза кадавра (а это 2 часа в лучшем случае, потому что в
пайплайне гоняются автотесты на новой версии кадавра), потом поднять версию
пакета в проекте и найти какого-нибудь дежурного, который подмержит новую версию в
мастер.

С одной стороны 3 часа - не смертельно, а с другой у нас вроде бы цель улучшить TTM.

>Поэтому еще раз. Если можно без кадавра - делаем без кадавра
