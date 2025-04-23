# Типичный тест

В самом базовом виде, тест-файл содержит следующие блоки:

- `beforeAll` - для инициализации зеркала сред (`Mirror`) и его слоев
- `afterAll` - для очистки mirror.
- `it` - блоки с тестами. Рекомендуется при большом их количестве группировать по смыслу в `describe`-подблоки, для улучшения читаемости ваших тест-файлов. 
- `beforeEach` - для инициализации контекста и, иногда, состояния кадаврика (если он одинаков для всех тестов)

__Примечание: Существует негласная договоренность не использовать функцию `test` для описания блоков с тестами. Ничего страшного в этом нет, но лучше если везде будет одинаково, т.е. `it`__


В качестве примера реализуем тест для виджета [WishList](https://a.yandex-team.ru/arc_vcs/market/front/apps/marketfront/market/platform.desktop/widgets/content/Wishlist/index.js):

В примере поочерёдно отражены два разных подхода к написанию тестов:
1) используя селекторы из `pageObject`-ов, которые достались нам в наследие от Hermione-тестов
2) используя атрибуты ролей и тестовые идентификаторы (`data-auto`)

В рамках тестов на Testament-е работают оба этих подхода, однако мы призываем уходить от использования `pageObject`-ов и переносить логику на второй, более прогрессивный способ -- ролевую модель элементов интерефейса, либо тестовые идентификаторы.

```js

import {fireEvent, screen, within, waitFor} from '@testing-library/dom';
import {makeMirrorDesktop} from '@self/root/src/helpers/testament/mirror';

//Page Object. Понадобится для написания querySelector-ов на определенные элементы DOM-дерева виджета. Таких как:
// - `root` - корень
// - `title` - блок с заголовком
// - `titleLink` - ссылка заголовка
// - `mainPrice` - блок с ценой
// - `shopRating` - блок с рейтингом
import SearchSnippetCell from '@self/project/src/components/Search/Snippet/Cell/__pageObject';

//Моки
import {createWishlistItem} from '@self/platform/widgets/content/Wishlist/__spec__/mocks';
import {createOffer} from '@yandex-market/kadavr/mocks/Report/helpers';
import {offerDSBSMock} from '@self/platform/spec/hermione/fixtures/dsbs';

//Декларации типов будут полезны для "автокомплита" в вашей IDE.
/** @type {Mirror} */
let mirror;
/** @type {JestLayer} */
let jestLayer;
/** @type {MandrelLayer} */
let mandrelLayer;
/** @type {ApiaryLayer} */
let apiaryLayer;
/** @type {KadavrLayer} */
let kadavrLayer;

const widgetPath = '..';

beforeAll(async () => {
    mirror = await makeMirrorDesktop({
        jest: {
            testFilename: __filename,
            jestObject: jest,
        },
    });
    jestLayer = mirror.getLayer('jest');
    mandrelLayer = mirror.getLayer('mandrel');
    apiaryLayer = mirror.getLayer('apiary');
    kadavrLayer = mirror.getLayer('kadavr');

    await jestLayer.backend.runCode(() => {
        //Внутри backend.runCode недоступны никакие замыкания, объявленные снаружи (например модули), поэтому требуется их явно инициализировать прямо внутри функции.  
        const mockResource = require('@self/root/src/helpers/testament/mockResource').default;
        
        // Мокаем конкретную функцию deleteWishlistItem
        mockResource('@self/root/src/resources/wishlist/', 'deleteWishlistItem', () => ({success: true}));
    }, []);
});

beforeEach(async () => {
    await mandrelLayer.initContext({
        request: {
            cookie: {
                // Кука с ID сессии кадавра. Обязательная часть инициализации, если ваш виджет
                // вызывает какие-нибудь резолверы. Без этой куки хост запроса не будет подменяться
                // и приложение будет пытаться ходить в реальные бекенды.
                kadavr_session_id: await kadavrLayer.getSessionId(),
            },
        },
    });
    await kadavrLayer.setState('report', createOffer(offerDSBSMock, offerDSBSMock.id));
    await kadavrLayer.setState('persBasket', createWishlistItem(offerDSBSMock.id));
});

afterAll(() => {
    mirror.destroy();
});

describe('Выдача. Гридовый список сниппетов', () => {
    // 1 часть. Подход к написанию тестов с использованием PageObject и querySelector
    describe('DSBS-оффер. Снипет DSBS товара', () => {
        it('должен отображаться', async () => {
            const {container} = await apiaryLayer.mountWidget(widgetPath);
            const root = container.querySelector(SearchSnippetCell.root);
            expect(root).toBeVisible();
        });

        describe('Заголовок', () => {
            it('содержит имя товара', async () => {
                const {container} = await apiaryLayer.mountWidget(widgetPath);
                const title = container.querySelector(SearchSnippetCell.title);
                expect(title.textContent).toContain(offerDSBSMock.titles.raw);
            });

            it('содержит верную ссылку и атрибут target', async () => {
                const {container} = await apiaryLayer.mountWidget(widgetPath);
                const titleLink = container.querySelector(SearchSnippetCell.titleLink);
                expect(titleLink.target).toContain('_blank');
                expect(titleLink.href).toContain(offerDSBSMock.urls.offercard);
            });
        });

        describe('Цена', () => {
            it('отображается', async () => {
                const {container} = await apiaryLayer.mountWidget(widgetPath);
                const price = container.querySelector(SearchSnippetCell.mainPrice);
                expect(price.textContent.replaceAll(/\D/g, '')).toBe(offerDSBSMock.prices.value);
            });

            it('содержит верную ссылку и атрибут target', async () => {
                const {container} = await apiaryLayer.mountWidget(widgetPath);
                const price = container.querySelector(SearchSnippetCell.mainPrice);
                expect(price.target).toContain('_blank');
                expect(price.href).toContain(offerDSBSMock.urls.offercard);
            });
        });

        // 2 часть. Подход к написанию тестов с использованием ролей и идентификаторов
        describe('Фото', () => {
            it('отображается', async () => {
                await apiaryLayer.mountWidget(widgetPath);
                const img = within(screen.getByRole('article')).getByRole('img');
                expect(img).toBeVisible();
            });

            it('содержит верную ссылку и атрибут target', async () => {
                await apiaryLayer.mountWidget(widgetPath);
                const imgLink = within(screen.getByRole('article')).getByRole('img');
                expect(imgLink.parentNode.target).toContain('_blank');
                expect(imgLink.parentNode.href).toContain(offerDSBSMock.urls.offercard);
            });
        });

        describe('Название магазина', () => {
            it('отображается и содержит название магазина', async () => {
                await apiaryLayer.mountWidget(widgetPath);
                const shopInfo = screen.getByRole('shop-name');
                expect(shopInfo).toBeVisible();
                expect(shopInfo.textContent).toContain(offerDSBSMock.shop.name);
            });

            it('содержит верную ссылку и атрибут target', async () => {
                await apiaryLayer.mountWidget(widgetPath);
                const shopInfo = within(screen.getByRole('shop-name')).getByRole('link');
                expect(shopInfo.target).toContain('_blank');
                expect(shopInfo.href).toContain(offerDSBSMock.urls.offercard);
            });
        });

        describe('Текст о количестве отзывов', () => {
            it('содержит ожидаемый текст', async () => {
                await apiaryLayer.mountWidget(widgetPath);
                const ratingCount = screen.getByRole('rating-count');
                expect(ratingCount.textContent).toMatch(/3\s219\sотзывов/);
            });
        });

        describe('Текст о доставке', () => {
            it('содержит "доставит продавец"', async () => {
                await apiaryLayer.mountWidget(widgetPath);
                const deliverInfo = screen.getByRole('delivery-info');
                expect(deliverInfo.textContent).toContain('доставит продавец');
            });
        });

        describe('Сердечко', () => {
            it('удаляет из избранного', async () => {
                await apiaryLayer.mountWidget(widgetPath);
                const heartButton = screen.getByTestId('wishlist-button');

                expect(heartButton.dataset.isChecked).toBe('true');

                fireEvent.click(heartButton);
                await waitFor(() => {
                    expect(heartButton.dataset.isChecked).toBe('false');
                });
            });
        });
    });
});
```
