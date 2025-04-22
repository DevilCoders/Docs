#Модуль OfferInfo

## Что умеет
По айдишнику получить базовую информацию об офере. 
Если офер приматчен к модельке, то возвращает ещё информацию о модельке

## Как

```js
var offerId = this.request.params.offerId;

this
    .push(this.module(require('app/modules/OfferInfo'), {
        id: String(offerId),
        user: this.user,
        request: this.request
    }), 'OfferInfo')
    .push(setOffer);


    function setOffer(offerData) {
        var offer = offerData.getInfo();
    }
```

## Странности
Сейчас делается два запроса за офером, т.к. без hid к нам не приходят характеристики
