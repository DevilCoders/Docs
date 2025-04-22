#### Компонент PromoModalWindow

##### Общее Описание

Компонент `PromoModalWindow` реализует логику показа модальных окон, которые должны появиться сразу при загрузке страницы.
Этот компонент является оберткой над левитановским `ModalWindow`. В компоненте реализована синхронизация признака показа модалки
с `localStorage`. Для этого был добавлен обязательный prop: `localStorageKey: string` для указания ключа для хранения этого признака.
Если в `localStorage` уже хранится переданный ключ признака `props.localStorageKey`, то модальное окно показано не будет.

По дефолту модалки `PromoModalWindow` не будут отрисовываться при прогоне АТ. Для того, чтобы в АТ протестировать именно сценарии с участием конкретной модалки `PromoModalWindow`,
то нужно указать query-параметр `allowedPromoModals` со значением, которое мы передали в пропс `localStorageKey`, и данная модалка будет показываться в этом АТ.

Дополнительно можно запретить показ промо-модалки установив `query`-параметр `hidePromoModals=1` на страницу. Например, это может быть полезно при заходе на страницу пингером, которому появившаяся модалка может помешать получить заголовок страницы, 

_Пример создания исключения для модального окна в АТ:_ 
```javascript
{
    title: 'Информационный попап',
    id: 'marketmbi-6897',
    issue: 'MARKETPARTNER-27267',
    environment: 'kadavr',
    currentParams: {
        shop: ffSupplier,
        query: {
            platformType: PLATFORM_TYPE.SUPPLIER,
            campaignId: ffSupplier.campaignId,
            activeTab: 'supply-request',
            mockSupplierId: 478311,
            allowedPromoModals: 'supplyRequestsWelcome', //может быть массивом
        },
    },
}
```

_Пример использования компонента_
```javascript
import {PromoModalWindow} from '~/components/PromoModalWindow';

...

<PromoModalWindow localStorageKey={SUPPLY_REQUESTS_WELCOME} isOpen={isOpen} width={520}>
    ...
</PromoModalWindow>
```

