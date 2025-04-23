# DeliveryCustomizer

## Что это?

Логика опций для кастомизации доставки

## Примеры опций

### "Оставить у двери"

- Если зажать, то будет сброс оплаты на PREPAID ввиду бизнес-логики и здравого смысла
- Также для каждой корзины (для юзера по итогу - отдельная доставка) прорастет это в комментарии, что увидит курьер
- При этом считаем опцию доступной, если это поддерживает СД, указан курьерский способ доставки и сам адрес доставки
- Также идет проверка на максимальную сумму заказа, что указана в CMS (maxSum)


## Примечание

- Пока что приходит в виде [захардкоженного списка для каждого СД из CMS](https://nda.ya.ru/t/0k3991c443tFvu)
    > Будет отдельно [поправлено по задаче](https://nda.ya.ru/t/rdaQXAt644Lt67)

## См. также
- Макеты из figma
    > [touch](https://nda.ya.ru/t/9x_UzGiw44LqCU), [desktop](https://nda.ya.ru/t/WpTDTlGw44Lq3b)
- Компонент группировки посылок, где отображаются опции для каждой посылки (корзины)
    > `src/widgets/content/checkout/common/CheckoutParcels/README.md`
- Реализация отображения кастомайзеров доставки
    > `src/widgets/content/checkout/common/CheckoutParcels/containers/CheckoutCovid/README.md`
    >
    > Внутри указаны причины, почему пришлось продублировать реализацию контейнеров
- Реализация в старом чекауте
    > `pokupki/src/widgets/content/checkout/common/CheckoutCovid/index.js`
- Константы для deliveryCustomizers
    > `src/constants/deliveryCustomizer.js`
- Эпики для deliveryCustomizers
    > `src/epics/checkout/deliveryCustomizer/index.js`
- [Старый PR с базовой реализацией](https://nda.ya.ru/t/QVNMg-0N44LtC3)
