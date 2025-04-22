Попапчик для выбора услуг при покупке конкретного товара
====

Использовать через контейнер `src/containers/PopupChoosingService`

При выборе новой услуги и нажатии кнопки сохранить - бросает глобальный экшен '@marketfront/SELECT_OFFER_SERVICE'.

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
    /** Колбек на простое закрытие попапа */
    closePopup: () => void,
}
```

Если у товара нет услуг, то попап не показывается.
