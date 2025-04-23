#### Сущность promoCodeDescription

Представляет собой сериализацию описания акции из `Loyalty`.

#### Формат

```javascript
const promoCodeDescription = {
    // shopPromoId акции из YT
    shopPromoId: 'L12345',
    // Величина скидки в процентах
    percent: 0,
    // Абсолютная величина скидки
    absolute: 1000,
    // Промокод
    code: 'MINUS1000',
    // Ссылка на страницу с правилами
    url: '',
    // Ссылка на лэндинг
    landingUrl: '',
    // Дата начала акции
    startDate: '01.07.2019',
    // Дата завершения акции
    endDate: '31.07.2022',
};
```
