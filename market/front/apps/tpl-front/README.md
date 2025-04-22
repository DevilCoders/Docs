# tpl-front

Удалим эту строчку в откате

[![Test Coverage](https://github.yandex-team.ru/pages/market/partnernode/coverage.svg)](https://github.yandex-team.ru/pages/market/partnernode/coverage/)

Партнерские интерфейсы на платформе **Node.js** (актуальная версия указана в `.nvmrc`).

## React

-   [Сборка на webpack](https://github.yandex-team.ru/market/partnernode/blob/master/configs/webpack/README.md)
-   [Документация по форме](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/components/FinalForm/README.md)
-   [Reselector Hash Table](https://pages.github.yandex-team.ru/market/partnernode/reselector)

## Code Style

Кодстайл проверяется по общемаркетным правилам

-   Для серверного кода: [market/codestyle](https://github.yandex-team.ru/market/codestyle)
-   Для клиентского кода: [market/workflow – .eslintrc.js](https://github.yandex-team.ru/market/workflow/blob/master/.eslintrc.js)

В дальнейшем (когда везде будет ES6) будет использоваться только
[market/codestyle](https://github.yandex-team.ru/market/codestyle)

Автопроверка кодстайла работает на push в репозиторий и осуществляется джобой
[market-frontend-partnernode-codestyle](http://cimarket.haze.yandex.net/job/market-frontend-partnernode-codestyle/),
которая просто выполняет скрипт [scripts/codestyle.bash](scripts/codestyle.bash) с аргументом `-r`

Ошибки автопроверки кодстайла должны быть устранены до прохождения ревью и мержа PR

Для проверки кодстайла локально можно в корне рабочей копии выполнить команду

```bash
make codestyle
```

Она вызывает тот же самый скрипт. Рабочая копия в этот момент должна быть собрана, т.к. кодстайл использует dev-зависимости.

Для создания новой страницы на реакте (с серверной частью) полезно использовать команду

```bash
make react-page
```

Команда спросит о базовых параметрах страницы и создаст все нужные файлы по рекомендованной структуре,
включая страничный модуль, реакт-компоненты, экшены, редюсеры, юнит-тесты и e2e-тесты, а также добавит
роут новой страницы в конфиг (так что созданная страница сразу будет открываться и работать).

У `make react-page` есть два варианта — либо страница с примерами проброски полей в стейте
(от резолверов до эпиков), с примером использования удалённого резолвера, селекторов,
экшенов с payload (для знакомства с принятыми практиками), либо пустая страница с пустым стейтом
и миниумом кода (для старта разработки новой страницы).

## I18n

[Про танкер на вики](https://wiki.yandex-team.ru/Market/Verstka/Partner/docs/integration/tanker/)

[Полезные хелперы для использования в текстах в танкере (в т.ч. для вставки разметки в текст)](https://wiki.yandex-team.ru/Market/frontend/Partner/docs/integration/tanker/#dokumentacijapoljambdamdljamustasha)

Подсказки выгружаются в [Бункер](https://wiki.yandex-team.ru/verstka/tools/bunker/)

При каждом запросе локальная версия подсказок сравнивается с версией подсказок в бункере, и, при необходимости, локальная версия обновляется

Также есть бэкап выгрузки бункера на случай, если бункер по какой-то причине недоступен.
Бэкап нужно обновлять вручную, запуская команду `make i18n` (после этого нужно запушить бэкап в репозиторий)

### React

#### В route страницы

Чтобы локализация в React-компонентах заработала, необходимо в route страницы указать параметр `pageId` внутри pageData:

```
...
pageData: {
    authOnly: true,
    pageId: 'stat-orders',
},
...
```

`pageId` должен быть, переведенным в kebab-case, именем страницы из ~/client.next/pages/. Т.е. для страницы ~/client.next/pages/StatOrders/index.js
значение `pageId` должно быть `stat-orders`, для ~/client.next/pages/FooBarLol/index.js — `foo-bar-lol`, и т.д. Это обусловлено текущими
настройками `webpack`.

#### В компонентах

Для локализации React-компонентов есть контейнер `~/containers/I18n`.

Для получения локализованного значения, надо использовать именно название `I18n`. Т.е. внутри компонента получить перевод для ключа `keyset:key` можно так:

```
import I18n from '~/containers/I18n';


<I18n id="keyset:keyWithoutParams" />
```

А так НЕ получится, ключи для таких вариантов не подтянутся на клиент:

```
import Renamed from '~/containers/I18n';

<Renamed id="keyset:key" />
```

Компонент `I18n` возвращает HTML элемент, соответственно, использовать его для указания значения аттрибутам HTML элементов не стоит(title, placeholder, etc).

#### В компонентах (если нужна строка, например, для placeholder'а input'а)

Для локализации React-компонентов есть HOC ~/containers/withI18n, который добавляет в props обернутого компонента функцию i18n.
Для получения в обернутом компоненте локализованного значения, надо использовать `i18n` как tagged template literal. Tagged literal в свою
очередь возвращает функцию, принимающую параметры для переведенного текста. Т.е. внутри компонента получить перевод для ключа `keyset:key` можно так:

```
i18n`keyset:keyWithoutParams`();
i18n`keyset:keyWithParams`.with({param: 'value'});
```

На самом деле, во время транспиляции кода все места, в которых тэг i18n используется без последующего вызова полученной функции, будут
автоматически исправлены. Т.е. при локализации без параметров можно писать так:

```
i18n`keyset:keyWithoutParams`;
```

Все вместе:

```
import withI18n from '~/containers/withI18n';

const LocalizedHello = withI18n(({i18n}) => (
    <div>
        <h2>{i18n`test.keyset1:hello`.with({name: 'Fedor'})}</h2>
        <p>{i18n`test.keyset1:glad.to.see.you`}</p>
    </div>
));
```

## Testing

### Unit tests

Все юнит-тесты лежат в директории [spec/unit](spec/unit), повторяя файловую структуру проекта
Запуск юнит-тестов производится командой:

```bash
make test
```

### Integration tests

Читаем [cookbook](https://github.yandex-team.ru/market/partner-cookbook).

#### Известные проблемы

Была ошибка с сертификатом в **Firefox'е 54 (64-бит)**, возможно это локальная проблема при запуске
под macOS, но точно пока не известно. Проблему обошли указанием в
[configs/development/ginny.conf.js](configs/development/ginny.conf.js) браузера **chrome**

```diff
--- a/configs/development/ginny.conf.js
+++ b/configs/development/ginny.conf.js
@@ -10,9 +10,9 @@ module.exports = {
             }
         },
         browsers: {
-            firefox: {
+            chrome: {
                 desiredCapabilities: {
-                    browserName: 'firefox'
+                    browserName: 'chrome'
                 }
             }
         },
```

## Настройка [deps-diff](https://github.yandex-team.ru/extg/deps-diff#deps-diff) для стартрека

1. Скопировать `.env` (он не под гитом, поэтому каждый может указать свой токен)

```bash
cp .env.example .env
```

2. [**Получить токен тут**](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b)

3. Прописать его в `.env`

## Документация внутри проекта

<!-- GENERATED_START(id:known-markdowns;hash:d777c25e4ce44aa113b427480c745843) This is generated content, do not modify by hand, to regenerate run "npm run generate:source:docs" -->
- [Страницы и виджеты](./app/README.md) ./app/README.md
- [Боковое меню](./app/resolvers/platform/sidebarMenu/README.md) ./app/resolvers/platform/sidebarMenu/README.md
- [Как мы пишем клиент](./client.next/Readme.md) ./client.next/Readme.md
- [Селекторница](./client.next/containers/Page/AutotestSelectorFinder/README.md) ./client.next/containers/Page/AutotestSelectorFinder/README.md
- [Боковое меню (клиент)](./client.next/containers/Sidebar/README.md) ./client.next/containers/Sidebar/README.md
- [CustomCashback (Кешбек на отдельные товары)](./client.next/pidgets/CustomCashback/README.md) ./client.next/pidgets/CustomCashback/README.md
- [CustomCashbackPromoForm (Форма группы кешбака на отдельные товары)](./client.next/pidgets/CustomCashbackPromoForm/README.md) ./client.next/pidgets/CustomCashbackPromoForm/README.md
- [ModalWindow (пиджет)](./client.next/pidgets/ModalWindow/README.md) ./client.next/pidgets/ModalWindow/README.md
- [PromoTreeSearch ](./client.next/pidgets/PromoTreeSearch/README.md) ./client.next/pidgets/PromoTreeSearch/README.md
- [Pidgets](./client.next/pidgets/README.md) ./client.next/pidgets/README.md
- [SamplePidget (Пример ридми)](./client.next/pidgets/SamplePidget/README.md) ./client.next/pidgets/SamplePidget/README.md
- [ShopInShopConstructor (Коструктор shop in shop)](./client.next/pidgets/ShopInShopConstructor/README.md) ./client.next/pidgets/ShopInShopConstructor/README.md
- [StandardCashback (Кешбек на весь ассортимент)](./client.next/pidgets/StandardCashback/README.md) ./client.next/pidgets/StandardCashback/README.md
- [SummaryAdvStrategiesAccount (Счет для рекламных стратегий)](./client.next/pidgets/SummaryAdvStrategiesAccount/README.md) ./client.next/pidgets/SummaryAdvStrategiesAccount/README.md
- [SummaryBusinessAlerts (Алерты на сводке маркетплейса)](./client.next/pidgets/SummaryBusinessAlerts/README.md) ./client.next/pidgets/SummaryBusinessAlerts/README.md
- [SummaryBusinessOpportunities (Возможности для бизнеса)](./client.next/pidgets/SummaryBusinessOpportunities/README.md) ./client.next/pidgets/SummaryBusinessOpportunities/README.md
- [SummaryBusinessQualityIndex (Индекс качества для бизнеса)](./client.next/pidgets/SummaryBusinessQualityIndex/README.md) ./client.next/pidgets/SummaryBusinessQualityIndex/README.md
- [SummaryCustomerCommunication (Общение с клиентами)](./client.next/pidgets/SummaryCustomerCommunication/README.md) ./client.next/pidgets/SummaryCustomerCommunication/README.md
- [SummaryDBSQualityAlert (Алерты на проблемы с качеством)](./client.next/pidgets/SummaryDBSQualityAlert/README.md) ./client.next/pidgets/SummaryDBSQualityAlert/README.md
- [SummaryExpiringOrders (Заказы с истекающим сроком доставки)](./client.next/pidgets/SummaryExpiringOrders/README.md) ./client.next/pidgets/SummaryExpiringOrders/README.md
- [SummaryGoodsStatUnited (Товары для единого каталога)](./client.next/pidgets/SummaryGoodsStatUnited/README.md) ./client.next/pidgets/SummaryGoodsStatUnited/README.md
- [SummaryListingContract (Договор на размещение)](./client.next/pidgets/SummaryListingContract/README.md) ./client.next/pidgets/SummaryListingContract/README.md
- [SummaryOrders (Заказы)](./client.next/pidgets/SummaryOrders/README.md) ./client.next/pidgets/SummaryOrders/README.md
- [SummaryOrdersDynamics (Динамика заказов)](./client.next/pidgets/SummaryOrdersDynamics/README.md) ./client.next/pidgets/SummaryOrdersDynamics/README.md
- [SummaryPartnerQualityIndex (Индекс качества для магазина)](./client.next/pidgets/SummaryPartnerQualityIndex/README.md) ./client.next/pidgets/SummaryPartnerQualityIndex/README.md
- [SummaryPendingOrders (Заказы, требующие подтверждения)](./client.next/pidgets/SummaryPendingOrders/README.md) ./client.next/pidgets/SummaryPendingOrders/README.md
- [SummaryProceed (Выручка)](./client.next/pidgets/SummaryProceed/README.md) ./client.next/pidgets/SummaryProceed/README.md
- [SummaryPromotionContract (Договор на продвижение)](./client.next/pidgets/SummaryPromotionContract/README.md) ./client.next/pidgets/SummaryPromotionContract/README.md
- [SummaryReturnsOrders (Невыкупленные заказы)](./client.next/pidgets/SummaryReturnsOrders/README.md) ./client.next/pidgets/SummaryReturnsOrders/README.md
- [SummaryStocks (Товары на платном хранении)](./client.next/pidgets/SummaryStocks/README.md) ./client.next/pidgets/SummaryStocks/README.md
- [Конфигурации окружения Маркета](./configs/README.md) ./configs/README.md
- [Сборка на wepback](./configs/webpack/README.md) ./configs/webpack/README.md
- [Скрипты сборки](./scripts/README.md) ./scripts/README.md
- [Выгрузка роутов в бункер](./scripts/routes-upload/README.md) ./scripts/routes-upload/README.md
- [Работа с нормализованными коллекциями](./shared/collections/README.md) ./shared/collections/README.md
- [Резолверы](./shared/resolvers/README.md) ./shared/resolvers/README.md
- [Удалённые резолверы для Яндекс Доставки 3.0](./shared/resolvers/delivery/README.md) ./shared/resolvers/delivery/README.md
- [Написание безопасных удаленных резолверов](./shared/utils/createSafeResolver/README.md) ./shared/utils/createSafeResolver/README.md
- [Автотесты в ПИ](./spec/README.md) ./spec/README.md
- [Написание тестов](./spec/gemini/README.md) ./spec/gemini/README.md
<!-- GENERATED_END(id:known-markdowns) -->
