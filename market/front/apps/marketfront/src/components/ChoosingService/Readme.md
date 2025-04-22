Скроллбокс выбора услуг при покупке конкретного товара
====

Использовать через контейнер `src/containers/ChoosingService`

При выборе новой услуги бросает глобальный экшен '@marketfront/SELECT_OFFER_SERVICE'.

Передает объект:

```javascript
{
    /** id cartItem-а для которого выбрали услугу */
    cartItemId: CheckoutCartItemId,
    /** id товара для которого выбрали услугу */
    offerId: OfferId,
    /** id выбранной улсуги (undefined если услуга удалена) */
    serviceId: OfferServiceId,
}
```

Контейнер принимает следующие параметры:
```javascript
{
    /** id cartItem-а для которого выбирается услуга */
    cartItemId: CheckoutCartItemId,
    /** Id товара для которого выбирается услуга */
    offerId: OfferId,
    /** Текущая выбранная услуга */
    selectedServiceId: OfferServiceId,
}
```

Если у товара нет услуг, то блок не показывается.
