# CheckoutParcel

## Что это?

Виджет посылки, может содержать несколько товаров из корзины.

- Логика редактирования информации по каждой корзине
    > Адрес / Способ доставки и прочие опции

## Что внутри?

### Parcel

Корзина со специфичными для себя параметрами (например, опция "Оставить у двери", "Адрес доставки")

#### CheckoutCovid

COVID опции доставки

- `LeaveAtDoor` - "Оставить у двери"
- ~~`Contactless` - "Бесконтактная доставка" (пока не поддерживается)~~

> **Примечание:**
> - Реализация взята из старого чекаута `pokupki/src/widgets/content/checkout/common/CheckoutCovid`
> - Содержит промежуточный контейнер-прослойку в виде "CheckoutCovid", т.к. там заложена общая логика, которая пригодится для будущих опций доставки
>   - (некоторые из которых уже есть в CMS, а другие - в ближайших планах)
