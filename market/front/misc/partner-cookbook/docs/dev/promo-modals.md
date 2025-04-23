# Промо модальные окна

### Общее описание
Промо модальные окна - это диалоговые окна, которые появляются сразу при открытии страницы ПИ.
Для таких модальных окон был написан отдельный компонент: 
```javascript
import {PromoModalWindow} from '~/components/PromoModalWindow';
```

Этот компонент является оберткой над левитановским `ModalWindow`. В компоненте реализована синхронизация признака показа модалки
с `localStorage`. Для этого был добавлен обязательный prop: `localStorageKey: string` для указания ключа для хранения этого признака.
Если в `localStorage` уже хранится переданный ключ признака `props.localStorageKey`, то модальное окно показано не будет.

```ts
<PromoModalWindow isOpen={isOpen} width={650} className={css.modal} localStorageKey="my-awesome-modal">
  content fot the modal
</PromoModalWindow>
```

По дефолту модалки `PromoModalWindow` не будут отрисовываться при прогоне АТ. Для того, чтобы в АТ протестировать именно сценарии с участием конкретной модалки `PromoModalWindow`,
то нужно указать query-параметр `allowedPromoModals` со значением, которое мы передали в пропс `localStorageKey`, и данная модалка будет показываться в этом АТ.

Например, для того, чтоб протестировать сценарии с промо модалкой из примера выше, то нужно добавить query-параметр `allowedPromoModals=my-awesome-modal`:
```ts
currentParams: {
    shop: ffSupplier,
    query: {
        ...
        allowedPromoModals: 'my-awesome-modal',
    },
},
```
И этот параметр подставится в урл: ```https://partner.market.fslb.yandex.ru/shop/1001140117/summary?allowedPromoModals=my-awesome-modal``` и модалка будет открываться в АТ, 



Дополнительно можно запретить показ промо-модалки установив `query`-параметр `hidePromoModals=1` на страницу.
Например, это может быть полезно при заходе на страницу пингером, которому появившаяся модалка может помешать получить заголовок страницы.

Например, если зайти на страницу по урлу ```https://partner.market.fslb.yandex.ru/shop/1001140117/summary?hidePromoModals=1```, то показ промомодалки не произойдет

|query параметр|Описание|Тип|
|:----------|:-------------|-------------:|
|allowedPromoModals=supplyRequestsWelcome|Включает показ промо модалки в АТ по идентификатору|string,string[]|
|hidePromoModals=1|Отключает показ промо модалок на странице|boolean|