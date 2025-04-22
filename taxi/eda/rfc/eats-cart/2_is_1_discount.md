Проблема:
Есть проблема в отображении товаров со скидкой "2 по цене 1". Т.к у нас часть товаров идут по полной цене, а часть товаров по нулевой, то существуют проблемы с оптимистичным ui относительно итоговой стоимости всех товаров, которая высчитывается на клиентах как qunatity * price. Если все так и оставить, то могут возникнуть неточности из-за того, что price за один товар динамически меняется в зависимости от количества товаров в корзине. 

Данная проблема встречается:
1. На экране корзине -> при увеличении количества айтемов работает оптимистичный ui по полю price
1. На экране товара в меню -> при увеличении количества айтемов работает оптимистичный ui по полю price

Решение:
На клиентах надо отключить оптмистичный ui по price, при увелечении/уменьшении количества товаров:
1. На экране корзине надо сделать шиммер на итоговой стоимости товаров. А также вместо того, чтобы считать стоимость всех товаров по одной позиции, как quantity * price, надо будет смотреть на новое поле `subtotal`, которое будет возвращаться в ответе корзины в cart.items[].subtotal.
2. На карточке товара в меню также необходимо отключить оптимистичный ui по price. И вместо того, чтобы показывать price * quantity, просто показывать price. Данная доработка в меню на согласовании менеджеров.

Объект айтема станет выглядеть так:

```
        CartItem:
            description: Блюдо в корзине
            type: object
            additionalProperties: false
            required:
              - id
              - item_id
              - name
              - price
              - decimal_price
              - item_options
              - quantity
              - description
              - weight
              - place_menu_item
++            - subtotal
            properties:
                id:
                    description: Идентификатор блюда в корзине
                    type: integer
                    format: int64
                item_id:
                    description: Идентификатор блюда в меню
                    type: integer
                    format: int64
                name:
                    description: Название блюда
                    type: string
                price:
                    description: Зафиксирванная цена товара
                    type: integer
                    format: int64
                decimal_price:
                    description: Зафиксирванная цена товара с копейками
                    $ref: '../definitions.yaml#/components/schemas/Money'
                item_options:
                    description: Наборы включенных опций (например, набор специй -
                        острый/обычный)
                    type: array
                    items:
                        $ref: '#/components/schemas/ItemOptionsGroup'
                quantity:
                    description: Количество блюд
                    type: integer
++              subtotal:
++                  description: Итоговая стоимость всех товаров в этой позиции с учетом примененных акций.
++                  $ref: '../definitions.yaml#/components/schemas/Money'
                description:
                    type: string
                weight:
                    description: Вес, текстовое представление (например, 400 грамм)
                    type: string
                place_menu_item:
                    $ref: '#/components/schemas/MenuItem'
                promo_type:
                    description: Тип акции, в результате которой блюда оказалось в
                        корзине, например "1 + 1. Блюдо в подарок".
                    $ref: '#/components/schemas/PromoType'
                promo_price:
                    description: Цена за 1 блюдо/товар со скидкой
                    type: integer
                    format: int64
                decimal_promo_price:
                    description: Цена за 1 блюдо/товар со скидкой с копейк

        Money:
            type: string
            x-taxi-cpp-type: decimal64::Decimal<2>
            pattern: '^-?[0-9]+(\.[0-9]{1,2})?$'
            example: '"123456.78"'

```

