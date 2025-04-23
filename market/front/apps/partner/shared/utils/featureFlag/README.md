# Feature флаги через бункер (makeCheckFeatureFlagInBunker)

Если вам нужно:

-   скрыть какой-то функционал под флаг
-   иметь возможность выкатить фичу, но не показывать пользователям
-   иметь возможность открыться только на внутреннюю сеть
-   иметь возможность открыться только на процент пользователей, бизнесов, магазинов (id % 100)
-   иметь возможность открывать его по какому-то идентификатору (например по businessId, campaignId или uid)
-   иметь возможность бысто выключить фичу в экстренной ситуации

Можно воспользоваться этой функцией

## Использование

### Создаем ноду в бункере

Узел нужно создавать как дочернюю у узла [settings](https://bunker.yandex-team.ru/market-partner/settings)

##### MIME-тип

`application/json; charset=us-ascii`

##### Контент

```json
{
    "common": {
        "enabledForAll": false,
        "enabledForInternalNetwork": false,
        "enabledFor": [],
        "disabledFor": [],
        "enableForPercentage": 0
    },
    "development": {
        "enabledForAll": false,
        "enabledForInternalNetwork": false,
        "enabledFor": [],
        "disabledFor": [],
        "enableForPercentage": 0
    },
    "testing": {
        "enabledForAll": false,
        "enabledForInternalNetwork": false,
        "enabledFor": [],
        "disabledFor": [],
        "enableForPercentage": 0
    },
    "production": {
        "enabledForAll": false,
        "enabledForInternalNetwork": false,
        "enabledFor": [],
        "disabledFor": [],
        "enableForPercentage": 0
    }
}
```

##### Поля:

-   `enabledForAll` - рубильник вкл/выкл на всех
-   `enabledForInternalNetwork` - рубильник вкл/выкл на внутреннюю сеть
-   `enabledFor` - Список ID, на которые открывается функциональность. Это могут быть как shopId, так и campaignId, и businessId.
-   `enableForPercentage` - процент на который хочется раскатить фичу. Проверяется по остатку от деления значения id на 100
-   `disabledFor` - Список ID, на которые принудительно отключается функциональность.

### Создаем переменную с названием ноды в бункере

Желательно чтобы назание переменной было `<ИМЯ_НОДЫ_В_БУНКЕРЕ>`, для единообразия и чтобы проще было находить к какой настройке переменная относится

> Над переменной в комменте нужно указать ссылку на тикет, в которой будет удаляться данная настройка.

https://a.yandex-team.ru/arc/trunk/arcadia/market/front/apps/partner/shared/constants/featureFlag/nodeNames.ts

```ts
// @todo выпилить после открытия на всех https://st.yandex-team.ru/MARKETPARTNER-36976
export const FOOTER_INFO_IN_SIDEBAR = 'footer-in-sidebar';
```

### Принудительное отключение и включение фичи через куку

Для того чтобы вкл./выкл. можно добавить куку вида `<имя-ноды-в-бункере>_b_feature_enabled` со значением `true`, если нужно чтобы она была включена, или `false` - чтобы была выключена.

Также можно переключать фичи через сервисную кнопку `BF`. Там же можно сбросить все проставленные куки фич.

### Как пользоваться

#### На сервере

##### Создание

Создаются в папке `shared/resolvers/featureFlags` выглядят примерно так:

> То что папка называется `resolvers` исторически так сложилось. Позже все фичи переедут в более правильно названную папку

```ts
import makeCheckFeatureFlagInBunker from 'shared/utils/featureFlag/makeCheckFeatureFlagInBunker';
import {FOOTER_INFO_IN_SIDEBAR} from 'shared/constants/featureFlag/nodeNames';

export default makeCheckFeatureFlagInBunker(FOOTER_INFO_IN_SIDEBAR);
```

`makeCheckFeatureFlagInBunker` принимает в аргументы `settingName` - название узла в бункере (в примере `footer-in-sidebar`)

Далее возвращаемая функция принимает:

1. `context` - контекст мандреля, как в резолверах
2. `params` - объект с единственным полем(пока) `id` в который передается идентификатор (например по businessId, campaignId или uid) по которому будет проверятся в поле `enabledFor` (and another) доступность фичи

##### Вызов

Если фича нужна на всех страницах, то можно вызвать в хелпере [getFeatureFlags](https://a.yandex-team.ru/arc_vcs/market/front/apps/partner/app/stout/pages/utils/getFeatureFlags.ts), который в свою очередь вызывается в [makeHtmlPage](https://a.yandex-team.ru/arc_vcs/market/front/apps/partner/app/stout/pages/utils/makeHtmlPage.ts?rev=r9334253#L774). `featureFlags` это поле в стейте redux-а (app.featureFlags) который хранит ключ-значение, где ключ это имя узла бункера, а значение `boolean` вкл. фича или выкл.

Если фича нужна только на одной странице, нет смысла проверять фичу на каждой странице. Можно вызвать резолвер в методе `getInitialState` нужной страницы и положить также в `app.featureFlags`. Результаты `makeHtmlPage` и `getInitialState` смержатся в один стейт. [Пример](https://a.yandex-team.ru/arc_vcs/market/front/apps/partner/app/stout/pages/html/HtmlOrderInfo/getInitialState.ts?rev=r9385892#L197)

```ts
import {FOOTER_INFO_IN_SIDEBAR} from 'shared/constants/featureFlag/nodeNames';
import footerInfoInSidebarFeature from 'app/resolvers/featureFlags/footerInfoInSidebar';

// ... code

featureFlags: props({
  [FOOTER_INFO_IN_SIDEBAR]: footerInfoInSidebarFeature(ctx, {id: businessId})
}),

// ... code
```

#### На клиенте

##### Компонент

Есть компонент [Feature](https://a.yandex-team.ru/arc_vcs/market/front/apps/partner/client.next/components/Feature/index.ts). В него можно обернуть компонент фкнкционала и он будет рендерить его если `app.featureFlags[<имя-фичи>] === true`. Если нет такого поля или фича вернула `false` будет рендериться fallback (по дефолту `null`)

Использовать можно так:

```tsx
import {FOOTER_INFO_IN_SIDEBAR} from 'shared/constants/featureFlag/nodeNames';
import Feature from '~/components/Feature';

// ... code

<Feature name={FOOTER_INFO_IN_SIDEBAR} fallback={<div>Мой старый компонент</div>}>
    <div>Мой новый компонент</div>
</Feature>;

// ... code
```

Компонент принимает пропсы:
-   `name` - Имя фичи по которой будет проверяться
-   `fallback` - то, что будет рендерится в случае если нет фичи или она `false`

##### Селектор

Если определять значение настройки нужно не для рендера компонентов - можно использовать селектор. Создаются они в файле со всеми [селекторами фичей](https://a.yandex-team.ru/arc_vcs/market/front/apps/partner/client.next/selectors/app/featureFlags.ts?rev=r9385892) передавая туда только константу названия узла в бункере

```ts
export const footerInfoInSidebarFlagSelector = makeFeatureFlagSelector(FOOTER_INFO_IN_SIDEBAR);
```

Используется потом просто как обычный селектор

### PROFIT!!!

Что можно еще доделать в этом методе, но нужды пока небыло:

-   Переделать, то, как указывается тикет на выпил настройки
-   Переделать то как расказывается на процент -> https://st.yandex-team.ru/MARKETPARTNER-41522
-   что-то еще чего я не придумал

Нужно также придумать как не плодить настройки, а чтобы они регулярно удалялись

Если есть пожелания или критика, можно приносить сюда -> @ilyaromanov
