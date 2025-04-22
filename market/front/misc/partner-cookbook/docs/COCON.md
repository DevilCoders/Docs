[Презентация](https://wiki.yandex-team.ru/Market/frontend/Partner/docs/cocon/.files/cocon.pdf)

## Предпосылки

В ЛК есть [разные типы пользователей](https://github.yandex-team.ru/savstavr/slides-access-restriction/blob/gh-pages/index.md) и [разные типы кампаний](https://wiki.yandex-team.ru/users/pixel/Vse-magaziny-/). Всем им нужен разный набор страниц, чтобы управлять размещением на сервисах (Маркет, мобильное приложение). Некоторые страницы есть у нескольких типов кампаний, при этом может отличаться, например, набор полей в форме или колонок в таблице.

В конце 2018 года мы начали обсуждать возможность сделать "конструктор кабинетов" - штуку, которая бы позволила быстро создавать кабинеты (сейчас этих кабинетов уже много, и будет ещё больше). Кабинет в этом всём - кусок партнёрки, отвечающий за конкретный тип кампании (shop, supplier, crossborder, fmcg) или пользователя (менеджер, агентство, клиент). Здесь были проблемы как со стороны фронта, так и со стороны MBI. В основном мы решали проблему разруливания доступов (хотя в целом это получилось похоже на движениие в сторону CMS, но к этому мы придём позже, если решим, что надо).

Как мы разруливали доступы раньше:

1. MBI заводит [экшен](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/mbi-java-sec-csv/src/resources/ru/yandex/market/security/migration/csv/mbi-partner/permissions.csv) с необходимыми проверками доступности. Проверки могут быть как ролевые (например, `SHOP_ADMIN` или `PARTNER_READER`), так и платформенные (тип кампании, значение какого-нибудь параметра, включенная программа, например, `ALL_NOT_SUPPLIER_AND_DROPSHIP` или `CROSSBORDER_SHOPS`)
2. В конфиге роутов фронта ЛК [привязываем](https://github.yandex-team.ru/market/partnernode/blob/7171be44ca66b46d1e0e62e008b5194f1c5255af/configs/route/groups/quality.js#L23) страницу к этому экшену
3. Также, если страница в рамках кампании, в конфиге роутов [указываем](https://github.yandex-team.ru/market/partnernode/blob/7171be44ca66b46d1e0e62e008b5194f1c5255af/configs/route/groups/quality.js#L15-L17), каким типам кампании она доступна
4. При заходе пользователя в ЛК:
   4.1. Ходим в ручку `getCampaign` для получения типа кампании, если текущая страница ему недоступна - редиректим
   4.2. Ходим в ручку `getAllowedActions` с экшеном текущей страницы и смотрим, доступен ли он. Если недоступен - рисуем плашку "У вас нет доступа"

Какие проблемы с этим были:

1. Непонятно, по роли или по платформенному признаку недоступна страница. В первом случае мы хотим показать "У вас нет доступа", а во втором - редиректнуть
2. Если нужно скрыть/показать какое-то поле в форме по ролевому или платформенному признаку, нужно дополнительно на самой странице вызывать `getAllowedActions` с подходящим экшеном и проверять на странице, доступен ли он
3. При добавлении нового типа кампании нужно добавлять правила в экшены MBI и добавлять проверки и флаги в роуты (в том числе апишные) на стороне фронта ЛК. Это постоянно приводило к рассинхрону и что-то отваливалось
4. Платформенные проверки размазываются между фронтом ЛК и MBI. Чекер `CROSSBORDER_SHOPS` в MBI и флаг `isCampaignTypeCrossborder` на фронте

Как мы их решаем:

1. Разносим ролевые и платформенные признаки в разные поля, соответственно, в результате получаем 2 флага отдельно
2. Описываем в странице фичи (части функционала), у которых могут быть свои правила доступности (ролевые и платформенные). В результате получаем список фич с информацией о том, доступна ли каждая из них
3. Новые роуты делаем вида `/<platformType>/<campaignId>/route-name`, и [рулим редиректами](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/app/stout/pages/abstract/platform/BasePlatformPage/utils/index.js#L24-L84) в зависимости от `platformType` и доступности страницы. Ну и от экшенов MBI отказываемся в пользу описания прямо в конфиге конкретных ролей и платформенных признаков (в принципе, это аналог экшенов, но мы должны его сделать понятнее и более тестируемым)
4. На фронте такие проверки будут не нужны, т.к. в конфиге конкретного типа кампании будут описаны только те страницы, которые доступны кампании. Нет роута = страница недоступна = редирект.

Также есть более глубокая проблема на бэкенде. Сейчас за всё, что связано с проверкой прав в ЛК отвечает конкретный бэкенд, заточенный под нужды ЛК (у нас MBI, у вендоров свой, у зарождающихся доставки и аналитической платформы тоже свои будут). И в каждом бэкенде копипастится система проверки прав (javasec). От этого тоже хочется уйти, поэтому как вариант развития видится вынесение в микросервис частей, отвечающих за регистрацию, контакты (пользователей, привязанных к кампании) и проверку прав.

## Конфигурация доступов

Под каждый тип кабинета создаётся конфиг в `json`
https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets
Пример конфига можно посмотреть [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json)
Типы можно посмотреть [здесь](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/app/types/platform.js)
Конфиг хранится (по крайней мере, пока что) в MBI. Это значит, что для изменения доступов нужно открыть PR в [репозиторий Cocon](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets). Вот [пример тикета в очереди MBI](https://st.yandex-team.ru/MBI-35656) на изменение конфига. В перспективе он переедет в микросервис, который будет отвечать за проверку прав (первый подход в проекте "Паспорт юридического лица").

В конфиге 3 уровня задания прав доступа:

- на весь конфиг
- на страницу
- на фичу

Все эти уровни при проверке объединяются через `И`. То есть, когда проверяем права на страницу, условие будет `[проверки на весь конфиг] И [проверки на страницу]`, а когда проверяем права на фичу - `[проверки на весь конфиг] И [проверки на страницу] И [проверки на фичу]`.
Но есть возможность указать флаг `override` на уровне страницы или фичи ([пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L11)), тогда все вышестоящие проверки не будут выполняться. То есть, указав `override: true` для фичи, получим условие `[проверки на фичу]`.

Описание полей (обязательные **выделены**):

### Конфиг [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json)

- **pages** <[`PageSchema[]`](#PageSchema)> - Описание страниц, которые доступны в рамках кабинета
- **roles** <[`ConditionRule<CheckerName>`](#ConditionRule)> - Ролевые правила
- **states** <[`ConditionRule<CheckerName>`](#ConditionRule)> - Платформенные правила [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L2-7)
- **features** <[`FeatureSchema[]`](#FeatureSchema)> - Описание фич, доступных на каждой странице кабинета [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/supplier.json?rev=r8424188#L10)

### Схема страницы [пример 1](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L9-68) [пример 2](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L221-263)

- **name** <`RouteName`> - Id роута из конфига роутера фронта
- **override** <`boolean`> - Признак того, что все вышестоящие правила нужно игнорировать [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L11)
- **roles** <[`ConditionRule<CheckerName>`](#ConditionRule)> - Ролевые правила [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L90-96)
- **states** <[`ConditionRule<CheckerName>`](#ConditionRule)> - Платформенные правила [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L135-140)
- **defaults** <[`$Shape<FeatureSchema>`](#FeatureSchema)> - Дефолтные правила для всех фич страницы, просто сахар, чтобы меньше копипастить. Если в конкретной фиче указаны собственные правила, они полностью перезатрут дефолтные правила (НЕ deep merge)
- **features** <[`FeatureSchema[]`](#FeatureSchema)> - Описание фич, доступных на странице [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L273-315)

### Схема фичи [пример 1](https://github.yandex-team.ru/market/partnernode/blob/7a4a4c07c4301d65ae8cf6bf6816cc623f6fed86/configs/platforms/shop/index.json#L12-L18) [пример 2](https://github.yandex-team.ru/market/partnernode/blob/7a4a4c07c4301d65ae8cf6bf6816cc623f6fed86/configs/platforms/shop/index.json#L19)

- **name** <`string`> - Название фичи
- **override** <`boolean`> - Признак того, что все вышестоящие правила нужно игнорировать
- **roles** <[`ConditionRule<CheckerName>`](#ConditionRule)> - Ролевые правила [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L111-116)
- **states** <[`ConditionRule<CheckerName>`](#ConditionRule)> - Платформенные правила [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L363-368)
- **params** <`Object`> - Произвольные параметры фичи [пример 1](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L287-289) [пример 2](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L57-59)
- **operations** <`string[]`> - Список ручек MBI, вызов которых инициирует эта фича (нужно MBI для проверки прав на ручки) [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L300-307)

### ConditionRule<ItemType> [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L13-18)

- **quantifier** <`'any' | 'all'`> - Через `ИЛИ` или через `И` объединять результаты вычисления правил
- **items** <`ItemType[]`> - Список правил для проверки

### Чекеры

Доступные в коконе чекеры (не все) (секция states)

В данной таблице описаны не все доступные чекеры - если не нашли чего-то на этой странице, то спросите явно в чатике кокона, а потом добавьте в эту таблицу, пожалуйста.

- IS_INTERNAL_NETWORK - разрешает только, если пользователь пришёл из внутренней сети (дружит с setIsInternalNetwork)
- ALLOWED_FOR_USERS - разрешает доступ только, если логин текущего пользователя входит в заданный список - для ограниченного бета-теста
- CAMPAIGN_TYPE - тип кампании клиента - SUPPLIER, SHOP, etc
- SUPPLIER_APP_STATUS - статус заявки юр. инфо (см. примеры в конфигах кабинетов)
- PARAM_VALUE - Проверка одного или нескольких [параметров](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/mbi-model/src/main/java/ru/yandex/market/core/param/model/ParamType.java) параметров, см. [для синих](https://wiki.yandex-team.ru/users/feoktistov/Razlichaem-ottenki-sinego/)
- ASSORTMENT_COMMITED - есть маппинг в MBO (каталог загружен и обработан)
- SUPPLIER_PLACEMENT_TYPE - deprectaed, будет удалён, вместо него нужно использовать PARTNER_PLACEMENT_TYPE
- PARTNER_PLACEMENT_TYPE - тип размещения поставщика в синем (дропшип/кросдок/клик-коллект/etc), [дока](https://wiki.yandex-team.ru/users/feoktistov/Razlichaem-ottenki-sinego/)
- SUPPLIER_WAREHOUSE_EXISTS - у клиента заведён склад
- SUPPLIER_FEED_EXISTS - у клиента загружен фид
- FEATURE - проверка [фичи](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/mbi-model/src/main/java/ru/yandex/market/core/feature/model/FeatureType.java) на статус (см. примеры в конфигах кабинетов), см. [для синих](https://wiki.yandex-team.ru/users/feoktistov/Razlichaem-ottenki-sinego/)
- MODEL_MANAGING_SHOP - неизвестно, значения - BATCH, MANUAL
- ~~SUPPLIER_DROPSHIP~~ - deprecated, см. PARTNER_PLACEMENT_TYPE
- ~~DROPSHIP_WITHOUT_STOCKS~~ - deprecated, см. PARTNER_PLACEMENT_TYPE
- ~~ALL_EXCEPT_DROPSHIP~~ - deprecated, см. PARTNER_PLACEMENT_TYPE
- SHOP_WORKFLOW_NEWBIE - клиент - "новичок", ему отображается визард (параметр IS_NEWBIE=true)
- VIRTUAL_SHOP - виртуальный магазин
- PROD_CAMPAIGN_ID - Определенные id кампаний, для тестинга отдаст true (PROD_CAMPAIGN_ID(1,2,3))

## Как использовать

### Node.js

Новые роуты создаём в [платформенной папке](https://github.yandex-team.ru/market/partnernode/tree/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/configs/route/platform) (просто для удобства там доопределяются необходимые [данные](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/configs/route/platform/index.js#L13-L19) и [регулярки](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/configs/route/platform/campaign/index.js#L18-L21)). Если роут в рамках кампании, его нужно положить в `configs/route/platform/campaign` [пример](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/configs/route/platform/campaign/outlet.js#L10-L24)

Сами новые html-страницы наследуем от [`HtmlPlatformPage`](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/app/stout/pages/abstract/platform/HtmlPlatformPage.js), т.к. там как раз и реализованы все проверки доступов по-новому (и поэтому новые страницы не надо [декорировать `app/stout/decorators/CheckAccess`](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/app/stout/pages/html/HtmlBadUrls/index.js#L22)).
**Важно**: в рамках одного проекта могут жить одновременно и новые кабинеты, и старые, так что если вам нужно сделать так, чтобы страница была доступна и в новом, и в старом кабинете - смотрите FAQ ниже. Примечание: Просто взять и перепилить эту страницу на `HtmlPlatformPage` нельзя, т.к. там не просто меняются проверки доступности этой страницы, там ещё и изменяются проверки доступности хлебных крошек и роутов сайдбара.

У html-страниц есть метод [`resolvePageFeatures`](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/app/stout/pages/utils/makeHtmlPage.js#L246), который возвращает промис с фичами. В резолверы нужно прокидывать руками. **TODO** Надо обсудить, как можно тут удобнее сделать (при этом не забыть, что когда дёргаем резолверы с клиента, routeName будет `market:api-resolve`)
[Пример](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/app/stout/pages/html/HtmlOrganizationInfo/buildInitialState.js#L10)
Ручки MBI, которые мы используем для получения вычисленных прав по страницам: https://swagger.market.yandex-team.ru/#/cabinet-controller

### React

На страницы, присутствующие в конфиге, приезжают фичи в поле `app.state.features`
Для удобной работы с ними есть [хоки](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/client.next/components/withFeatures/index.js), [селекторы](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/client.next/components/withFeatures/selectors.js) и [общие утилиты](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/shared/utils/platform/index.js) (**TODO** надо как-то подружить селекторы и утилиты, доку обновлю потом)
[Пример 1](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/client.next/pages/CommonInfo/components/Analytics/index.js#L27) [Пример 2](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/client.next/pages/CommonInfo/components/ShopInfo/ShopWebsite/index.js#L61)


## Релиз кокона
1. Зайти в свой pull request в [Arcanum](https://a.yandex-team.ru)
2. Нажать на кнопку **Merge** и включить галочку **Enable automatic merging**
3. Необходимо зайти на [страницу релизной машины кокона](https://tsum.yandex-team.ru/pipe/projects/market-b2b/delivery-dashboard/market-b2b-cocon)
4. Увидеть свой PR в очереди и дождаться, пока пайплайн сборки дойдет до блока (кубика) под названием **"В прод"**
5. Проверить в [тестинге партнёрки](https://partner.market.fslb.yandex.ru), что изменения в коконе работают как ожидается
6. Нажать кнопку **"Play"** (Или просто снять Гендальфа и не ждать, пока прогон дойдет до этого блока)
---

## FAQ

### Я замерджил свои правки в транк, но релиз почему-то стоит. Что делать?

- Зайди в [релизный пайплайн кокона](https://tsum.yandex-team.ru/pipe/projects/market-b2b/delivery-dashboard/market-b2b-cocon).
- Найди релиз, в который попали твои правки.
- Если перед твоим релизом есть другие релизы, у которых виден прогресс-бар, то нужно протолкнуть их все по-очереди, начиная с нижнего.
- Заходи в детали нужного релиза и смотри на состояние кубиков.
- Если какой-то кубик красный, то
  - если это кубик мониторинга, то попробуй перезапустить его самостоятельно;
  - если красный кубик - это не мониторинг, или кнопка перезапуска мониторинга заблокирована (у тебя нет прав), или перезапуск не помогает, то зайди в чат кокона и попроси посмотреть релиз.
- Если все кубики до кубика "в прод!" зелёные, а кубик "в прод!" серый, то нужно постучаться в личку всем разработчикам, чьи коммиты входят в этот релиз, и попросить их проверить правки на тестинге. Если всё ок, то кто-то из них должен снять гендальфа или запустить кубик "в прод!" вручную, тем самым запустив релизный пайплайн дальше.
- Продолжай наблюдать за пайплайном, и если будут красные кубики, то пиши в чат кокона.

### У меня есть задача "сделать новую страницу", делать ли мне её сразу на этой схеме?

Да, вот пример: https://github.yandex-team.ru/market/partnernode/pull/5531/commits/7bf903204741e5013e4ac5662d9c02ea147b969e

### У меня есть задача сделать что-то новое или поправить старое в конфигах кокона, но я хочу сначала протестировать свои правки перед тем, как пускать их на прод. Как мне это сделать?

Для тестирования правок в кокон-конфигах предусмотрена следующая схема:

- создаётся PR в коконе с нужными правками через [arc](https://arc-vcs.yandex-team.ru/docs/index.html) (ПР, созданные через веб-интерфейс, отлаживать нельзя)
- разработчик запоминает id последнего коммита
- использовать конфиги из PR можно одним из способов:
  - нажав на **C** в тулбаре в правом нижнем углу страницы, введя в input id коммита и нажав Enter
  - добавив в url query-параметра `cocon_commit_id` с id коммита
  - добавив куку `cocon_commit_id` с id коммита
- при создании демо-стенда можно указать id коммита, тогда указывать куку/параметра не нужно - кокон будет брать конфиги из коммита автоматически для автотестов (но просто при заходе на стенд нужно всё равно указывать коммит вручную, но это не точно)
- для АТ можно использовать переменную окружения `COCON_COMMIT_ID`. Например, `COCON_COMMIT_ID=d2fa2ff2335b1225c17daf109ba81d5427dcb46c AT_ID="marketmbi-1000" make autotest`

### Как понять, выехали ли мои правки в тестинг/прод?

Можно следить тут: https://tsum.yandex-team.ru/pipe/projects/market-b2b/delivery-dashboard/market-b2b-cocon

### Что делать, если моя страница должна быть доступна и в новом, и в старом кабинете

Нужно вынести тело страницы в [отдельный файлик](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/app/stout/pages/html/HtmlCommonInfo/buildInitialState.js#L11-L23), заюзать его в [старой](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/app/stout/pages/html/HtmlCommonInfo/index.js#L14) и [новой](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/app/stout/pages/html/platform/HtmlPlatformCommonInfo/index.js#L14) страницах.
Также нужно создать [роут для новой страницы](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/configs/route/platform/campaign/settings.js#L23-L34), но при этом оставить и [старый](https://github.yandex-team.ru/market/partnernode/blob/3f67c518fe319ab80ea9b4d42abbeb5998858b0d/configs/route/groups/commonInfo.js#L10-L24).
В конфиге кабинета нового типа указываем новый роут ([`fmcg`](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/fmcg.json#L265)), и для поддержики кабинетов старого типа указываем старый роут в их конфигах ([crossborder](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/crossborder.json#L179), [shop](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/shop.json#L285)). Ну, только в тех, в которых эта страница нужна, например, `feeds-list` не нужна для `supplier`, там её и не указываем.
Всё, теперь при [вызове `resolvePageFeatures`] на этой странице вам будут возвращаться фичи и при заходе под fmcg, и под crossborder, и под shop.

### Как сделать так, чтобы фича была доступна `shop`, но была недоступна `crossborder`?

В конфиге для `crossborder` её просто не нужно указывать. Например, [вот](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/shop.json#L448) фича у `shop`, которой [нет](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/crossborder.json#L252-295) у `crossborder`.

### Как переехать на схему, если бэк ещё не готов ?

Как переходное решение, можно запилить вычисление правил на фронте и на фронте же хранить конфиг. Получится [типа такого](https://github.yandex-team.ru/market/partnernode/blob/4d4f5cbe9551ef46830ae40963b1bb39e0da0efb/app/resolvers/platform/index.js#L39-L111)

### Можно ли использовать cocon_commit_id на престейбле ?

В данный момент - нет, но лучше посмотреть на обсуждения в [таске на MBI](https://st.yandex-team.ru/MBI-46005).

### Как коконизировать старую страницу?

Выполняем:
- Проверяем в конфиге кокона наличией этой страницы - возможно, она уже перенесена полностью или частично - [supplier.json для синих](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/supplier.json).
- Вычисляем права на страницу:
  - Ищем объявление роута страницы в `configs/route/**`, смотрим в поле `data.group` и переходим к описанию action'а
    ```javascript
    // ВНИМАНИЕ: в примерах используется вымышленный роут!

    {
      name: 'market-partner:file:fulfillment-supply-document:get',
      pattern: '/fulfillment/supply/doc(/)',
      data: {
        method: 'GET',
        pageName: 'HtmlFulfillmentSupplyDoc',
        isCampaignOnly: true,
        isCampaignTypeShop: true,
        isCampaignTypeSupplier: true,
        pageData: {
            authOnly: true,
            pageId: 'fulfillment-supply-doc',
            template: `${basePagesTemplatesPath}/fulfillment-supply-doc/fulfillment-supply-doc.yate`,
        },
        group: Groups.fooBar, // НАМ СЮДА
      },
    },
    ```
  - Из описания action'а (см. `configs/rights/groups.js`) берём его имя из поля `name`
    ```javascript
      fooBar: {
        name: '/foo/bar', // НАМ СЮДА
        isCommon: true,
        shopOnly: false,
        managerOnly: false,
      },
    ```
  - Ищем action в [permissions.csv](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/mbi-java-sec-csv/src/resources/ru/yandex/market/security/migration/csv/mbi-partner/permissions.csv)
    ```csv
      "/foo/bar","ALL_EXCEPT_DROPSHIP",""
      "/foo/bar","SUPPLIER_APP_STATUS","COMPLETED,FROZEN"
    ```
    Условия в этом файле вычисляются через `ИЛИ`. В первом столбце находится action, во втором - используемый чекер, в третьем - параметры для передачи в чекер. Чекер - функция, которая опционально принимает параметры и возвращает true/false.
  - Ищем описания используемых чекеров в [auth.csv](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/mbi-java-sec-csv/src/resources/ru/yandex/market/security/migration/csv/mbi-partner/auth.csv) - в первом столбце находится имя чекера, во втором - описание (но доверять на 100% ему нельзя потому, что всё меняется), в третьем - базовый чекер. Базовым чекером может быть статический чекер (trueAuthorityChecker всегда возвращает true, falseAuthorityChecker всегда возвращает false) или кастомный чекер, чья реализация лежит внутри MBI (подробности по ним нужно искать в исходниках или у разработчиков MBI).
    ```csv
    "ALL_EXCEPT_DROPSHIP","Служебная роль. Все кроме DROPSHIP","trueAuthorityChecker"
    "...","...","..."
    "SUPPLIER_APP_STATUS","Просмотр страницы каталог поставщика","supplierApplicationStatusChecker"
    ```
  - Ищем комбинаторное условие для чекера/чекеров из описания action в [auth_links.csv](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/mbi-java-sec-csv/src/resources/ru/yandex/market/security/migration/csv/mbi-partner/auth_links.csv)
    ```csv
    "ALL_EXCEPT_DROPSHIP","SUPPLIER_FEED_EXISTS","and",""
    "ALL_EXCEPT_DROPSHIP","SUPPLIER_APP_STATUS","and","COMPLETED,FROZEN"
    "ALL_EXCEPT_DROPSHIP","PARAM_VALUE","and","DROPSHIP_AVAILABLE:false"
    "...","...","...","..."
    "SUPPLIER_APP_STATUS","SUPPLIER_ROLES","and",""
    ```
    В первом столбце находится имя чекера, во втором - имя дополнительного чекера, в третьем - оператор объединения результата вызова данного дополнительного чекера с результатом вызова предыдущего чекера, в четвёртом - параметры вызова дополнительного чекера. Для первой строки описания чекера идёт объединение с результатом базового чекера (см. auth.csv выше), т.е.
    ```
    ALL_EXCEPT_DROPSHIP = trueAuthorityChecker and SUPPLIER_FEED_EXISTS and SUPPLIER_APP_STATUS(COMPLETED,FROZEN) and PARAM_VALUE(DROPSHIP_AVAILABLE:false)
    SUPPLIER_APP_STATUS = supplierApplicationStatusChecker(параметры-вызова-чекера) and SUPPLIER_ROLES
    ```
    С используемыми дополнительными чекерами знакомимся рекурсивно.
  - Так как одна и та же страница может использоваться в нескольких кабинетах (белый/синий/etc), то нужно определить, в каких же именно кабинетах используется коконизируемая страница.
  - Составляем условие для коконизированной страницы. Помним, что некоторые чекеры являются deprecated (см. таблицу выше), поэтому при сомнениях или вопросах лучше обратиться в чатик `Cocon. Конструктор кабинетов`. Так же помним, что кокон умеет вычислять только простые условия (`a && b && c` или `a || b || c`), поэтому при необходимости использовать более сложное условие нужно прийти в чатик. Если страница используется в нескольких кабинетах, то нужно вычислить правила доступа отдельно для каждого кабинета.
    ```javascript
      {
        // ...
        "states": {
          "quantifier": "all", // "all" для &&, "any" для ||
          "items": [
            // ALL_EXCEPT_DROPSHIP deprecated, поэтому раскрываем его
            "SUPPLIER_FEED_EXISTS",
            "SUPPLIER_APP_STATUS(COMPLETED,FROZEN)",
            "PARTNER_PLACEMENT_TYPE(-DROPSHIP)"
          ]
        }
      },
    ```
- Прописываем правила доступа к странице в коконе ...
  - ... в [supplier.json для синих](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/supplier.json):
    ```javascript
      {
        // Для удобства оставляем старое имя роута.
        "name": "market-partner:html:fulfillment-supply-document:get",
        // Стандартная секция для синих, копируем как есть.
        "roles": {
          "SHOP_ADMIN",
          "PARTNER_READER",
          "AGENCY"
        },
        // Выписываем вычисленные правила доступа.
        "states": {
          "quantifier": "all", // "all" для &&, "any" для ||
          "items": [
            // ALL_EXCEPT_DROPSHIP deprecated, поэтому раскрываем его
            "SUPPLIER_FEED_EXISTS",
            "SUPPLIER_APP_STATUS(COMPLETED,FROZEN)",
            "PARTNER_PLACEMENT_TYPE(-DROPSHIP)"
          ]
        }
      }
    ```
    Отправляем ПР. Так как мы добавляем новую страницу в кокон, наши правки не могут ничего задеть, и ПР можно сразу мерджить в мастер. После этого можно не заморачиваться с `cocon_commit_id` и свободно проверять коконизированную страницу на престейбле, если нужно.
- Правим саму страницу для коконизации:
  - `HtmlPage` заменяем на `HtmlPlatformPage`.
  - Удаляем декоратор `CheckAccess`.
  - Переносить файлы в другие каталоги не нужно.
  - В `getInitialState` и остальном серверном коде страницы меняем чтение параметра `id` на параметр `campaignId`
- Работаем с роутами:
  - Используем коконизацию - правим существующий роут:
    ```javascript
      {
        // То же имя роута, как в коконе - старое для удобства миграции.
        name: 'market-partner:html:fulfillment-supply-document:get',
        // Коконизированный шаблон - с platformType и campaignId,
        // а после них дописываем уникальную часть урла для нашей страницы.
        // Сохранять в дописанной части урла принадлежность к типу кабинета нет смысла
        // потому, что эта принадлженость отображена в platformType.
        pattern: '/<platformType>/<campaignId>/supply/doc',
        data: {
          // Выпиливаем часть полей, оставляем только указанные.
          method: 'GET',
          pageName: 'HtmlFulfillmentSupplyFile',
          // Эта часть остаётся без изменений.
          pageData: {
            authOnly: true,
            pageId: 'fulfillment-supply-doc',
            // Это поле лучше удалить и перевести страницу на SSR.
            template: `${basePagesTemplatesPath}/fulfillment-supply-doc/fulfillment-supply-doc.yate`,
          },
          // Если описание роута лежит не в папке platform, то добавляем это поле,
          // иначе роут не будет восприниматься роутером как платформенный.
          isPlatformPage: true,
        },
      },
    ```
  - Так как у пользователей могли остаться закладки в браузере на эту страницу, урл на страницу мог быть упомянут в хелпах и по другим причинам нам нужно сохранить работу старого урла страницы. Для этого в `configs/route/redirects.js` добавляем новый редирект со старого урла на новый коконизированный роут:
    ```javascript
      {
        // В имени старого роута меняем "html" на "redirect"
        name: 'market-partner:redirect:fulfillment-supply-document:get',
        // Урл от старого роута.
        pattern: '/fulfillment/supply/doc(/)',
        data: {
          method: 'GET',
          pageName: 'RedirectPage',
          pageData: {
            authOnly: true,
            redirectTo: 'market-partner:html:fulfillment-supply-document:get',
            redirectParams: {
              platformType: campaignPlatform.supplier,
            },
            redirectRule: {
              id: 'campaignId',
            },
          },
          // Сохранять здесь старую проверку не имеет смысла - новый роут уже
          // проверяет нужные права, ошибку лучше показать уже на новом роуте.
          group: Groups.default,
        },
      },
    ```
  - Если на странице есть кастомные ссылки на Помощь или хлебные крошки, то переносим их в файл `configs/platforms/supplier/index.json`.
- Правим клиентский и серверный код - ищем использование роута по коду
  - Ищем по коду чтение параметра `id` (например, напрямую из params) и заменяем на селектор `getCampaignId`.
  - Ищем по коду ссылки на роут и дополняем их, делая коконизированными:
    - `Link`-подобные компоненты заменяем на `PlatformLink`-аналоги
      ```
        <Link
          to="market-partner:html:fulfillment-supply-document:get"
          params={{id, docId}}
          target="_blank"
        >
          <I18n id="foo:bar" />
        </Link>

        <!-- нужно заменить на PlatformLink - platformType и campaignId будут подставлены автоматически -->
        <PlatformLink
          to="market-partner:html:fulfillment-supply-document:get"
          params={{docId}}
          target="_blank
        >
          <I18n id="foo:bar" />
        </PlatformLink>
      ```
    - В вызовах `buildUrl` (АТ или код) переименовываем параметр `id` в `campaignId` и добавляем нужный `platformType` (в сложных случаях можно указать произвольный `platformType` - на странице в любом случае произойдёт редирект на нужный `platformType`, но лучше всё-таки указывать):
      ```javascript
        const url = buildUrl('market-partner:html:fulfillment-supply-document:get', {
          campaignId: ctx.params.id,
          platformType: PLATFORM_TYPE.SUPPLIER,
        });
      ```
    - Ищем API-запросы со страницы, и если они есть, то
      - Вычисляем правила доступа до API-страницы - см. выше.
      - В описании страницы в коконе добавляем секцию `features`, в которую добавляем новую фичу для похода в API-страницу:
        ```javascript
          {
            // Наша страница в коконе.
            "name": "market-partner:html:fulfillment-supply-document:get",
            "roles": { /* Остаётся без изменений. */},
            "states": { /* Остаётся без изменений. */},
            // Добавляем или расширяем, если уже есть.
            "features": [
              {
                // Называем фичу в соответствии с семантикой API-вызова
                "name": "getting-something",
                // Описываем роли, если у API-страницы есть ограничения по ролям.
                // Если ограничений нет, то эту секцию не добавляем.
                "roles": { /* ... */ },
                // Добавляем описание правил доступа до API-страниц.
                "states": { /* ... */ },
                // К префиксу cocon/supplier добавляем часть из имени фичи - соглашение.
                "operations": [
                  "cocon/supplier/getting-something"
                ]
              }
            ]
          }
        ```
      - В файл с action'ами `configs/rights/groups.js` добавляем новую запись
        ```javascript
          const Groups = {
            // ...
            // Даём уникальное соответствующее имя.
            gettingSomething: {
                // Эта строка берётся из массива operations из описания фичи.
                name: 'cocon/supplier/getting-something',
                // Это копируем как есть.
                isCommon: true,
                shopOnly: false,
                managerOnly: false,
            },
            // ...
          };
        ```
      - В описании роута API-страницы меняем `data.group` на `Groups.gettingSomething`
- Правим ссылки в Танкере - ищем использование роута по всему [проекту](https://tanker.yandex-team.ru/?project=market-partner&branch=master), оставляем параметр `id`, чтобы публикацией не сломать ссылку на текущей странице на проде, добавляем `campaignId` и нужный `platformType`:
  ```
  было
  «[Текст ссылки]({{#_.buildUrl}}market-partner:html:fulfillment-supply-document:get|{"id": "{{id}}"}{{/_.buildUrl}})»
  стало
  «[Текст ссылки]({{#_.buildUrl}}market-partner:html:fulfillment-supply-document:get|{"id": "{{id}}", "campaignId": "{{id}}", "platformType": "supplier"}{{/_.buildUrl}})»
  ```
- Tips and tricks
  - Для подстановки значений в параметр `platformType` нужно использовать `PLATFORM_TYPE` из `shared/constants/campaign`.
  - По любым вопросам можно обращаться в чатик `Cocon. Конструктор кабинетов`.


## Обсуждения

<details>
<summary><b>На беседах о ПИ от 12.07.2022 на тему "Можем ли мы жить без кокона в каком-то режиме, если кокон лежит?"</b></summary>

**Проблема:**

Во время последнего факапа кокон лежал 2 часа, соответственно, были недоступны все страницы ПИ. Это сломало операционную деятельность магазинов - в частности, обработка заказов и отгрузок для FBS. У саппорта в админке реализована не вся функциональность, например, печать ярлыков, поэтому саппорт не мог помочь магазинам.

**Что хочется:**

Минимум - во время факапа кокона страницы/функциональность ПИ были бы доступны саппорту под внутренней сетью - возможно, с артефактами в интерфесе, но с рабочей функциональностью.

Максимум - во время факапа кокона магазины продолжают работать с ПИ с некоторыми допущениями - ПИ может не знать про переключения магазинов новичок/включен, отключен/включен.

Как мы улучшаем стабильностью кокона уже сейчас:

При каждом походе в кокон его ответ складывается в memcache, а при ошибках кокона данные достаются из кеша и возвращаются вместо ответа кокона.

Плюсы решения - ttl до 10-12 часов для 70-80% магазинов.
Минус решения - если магазин не заходил в ПИ, и его данных нет в кеше, то в ПИ будут 500-ки.

Это - режим с пост-использованием кеша.
Так же есть режим честного кеша.

**Решение 1:**

Для менеджеров и саппорта под внутренней сетью вместо ответов кокона всегда возвращать `true`.

Нюансы:
- для страниц states/roles мы можем подменять на `true`, с этим проблем нет
- для глобальных и страничных фич states/rols мы тоже можем подменять на `true`, но тогда в UI и резолверах могут быть спецэффекты (одновременное исполнение кода для всех платформ в некоторых случаях или исполнение код от одной платформы для магазина другой платформы), особенно актуально для isDropship/isFulfillment/isDropshipBySeller фич
- за счёт статичной подстановки `true` в `roles` ролевая модель будет потеряна
- для reader'ов мы сейчас запрещаем write-операции вне mbi (mbi умеет проверять роль ридера, а остальные подсистемы - нет), в случае подставноки `true` в `roles` reader'ы смогут выполнять все операции на странице без контроля
- для reader'ов мы скоро начнём проверять 2-х факторную авторизацию через кокон, поэтому если мы будем мокать ответ кокона, то мы начнём пускать reader'ов без 2-х факторной авторизации
- начнём для новичков и отключенных показывать функциональность, доступную только для включенных магазинов

**Решение 2:**

Периодически генерировать по uid/campaignId/cabinet/etc таблицу со значениями чекеров кокона во всех кабинетах. При факапе кокона получать из этой таблицы значение ответов кокона для фич/страниц.

Нюансы:
- перестанем реагировать на смену состояния магазина новичок/включен/отключен - будем использовать старое состояние на момент генерации таблицы

**Решение 3:**

Заменить memcache на серверах на redis в облаке, чтобы повысить ttl и снизить вымывание кеша.

Нюансы:
- перестанем реагировать на смену состояния магазина новичок/включен/отключен - будем использовать старое состояние на момент генерации таблицы
- тот же, что для memcache - если магазин не заходил, и мы не заполнили кеш для него, то он получит 500-ку

**Решение 4:**

Точечно замокать ответы кокона на одной странице, чтобы она продолжала работать во время факапа кокона. Например, страницу отгрузок.

Нюансы:
- даже если "отрезать" конкретную страницу от кокона, то попасть на неё можно будет только по прямому урлу потому, что остальные страницы и боковое меню будут лежать

**Разное**

Специальный режим "Safe mode" работает только для mbi-partner.

**Action items:**

Попробовать заменить memcache на redis - желающие и техсовы, но это не точно.

Попробовать какой-нибудь из вариантов мокания ответов кокона во время недоступности кокона в общем случае - желающие.

</details>
