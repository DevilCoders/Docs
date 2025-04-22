# Новые скидки в коре

## Задача

Мы плавно переносим скидки из коры в сервис eats-discounts, и поэтому необходимо отдавать информацию о новых скидках(скидки из eats-discounts) в кору, чтобы правильно записывать информацию о них в ревизии.

## Решение

Старые скидки, которые уже хранятся в коре, мы не трогаем, информацию о них мы продолжаем передавать в том же виде. А вот для новых скидок мы дорабатываем АПИ.

Информацию о скидках мы передаем в 4 internal ручки: `/internal/eats-cart/v1/create_cart`, `/internal/eats-cart/v1/get_cart`, `/internal/eats-cart/v1/lock_cart_pickup`, `/internal/eats-cart/v1/lock_cart`.
Для ручки `/internal/eats-cart/v1/create_cart` нам необязательно отдавать информацию о новых скидках т.к эта ручка используется только в скрипте переноса корзин.
Ручка `/internal/eats-cart/v1/get_cart` используется в админке, чтобы получить инфу о новой корзине, поэтому в этой ручке стоит отдавать информацию о новых скидках.
Ручки `/internal/eats-cart/v1/lock_cart(_pickup)` в том числе используются для создания ревизий, поэтому в этой ручке нам обязательно нужно передавать информацию о новых скидках.

Решили, что новые акции будут передаваться новых полях:
1. InternalCart.new_promos - Массив новых акций на корзину(акция при корзине от 1000 рублей). Эти акции надо будет размазывать на стороне ревизий.
1. ItemForCheckout.new_discounts - Массив новых скидкок на один айтем(скидка на айтем 100 рублей, подарочный айтем).

```

        InternalCart:
            type: object
            additionalProperties: true
            x-taxi-additional-properties-true-reason: allOf
            required:
              - cart_id
              - revision
              - shipping_type
              - items
              - promos
              - subtotal
              - total
              - discount
              - created_at
              - service_fee
++            - new_promos
            properties:
                cart_id:
                    type: string
                    description: ID корзины в БД eats_cart
                revision:
                    type: integer
                    description: |
                        номер ревизии корзины,
                        нужно передать в запросе на выставление номера заказа
                shipping_type:
                    $ref: '../definitions.yaml#/components/schemas/ShippingType'
                items:
                    type: array
                    items:
                        $ref: '#/components/schemas/ItemForCheckout'
                promocode:
                    $ref: '#/components/schemas/PromocodeForCheckout'
                promos:
                    type: array
                    items:
                        $ref: '#/components/schemas/PromoForCheckout'
                subtotal:
                    $ref: '../definitions.yaml#/components/schemas/Money'
                total:
                    $ref: '../definitions.yaml#/components/schemas/Money'
                discount:
                    $ref: '../definitions.yaml#/components/schemas/Money'
                order_nr:
                    type: string
                created_at:
                    type: string
                service_fee:
                    $ref: '../definitions.yaml#/components/schemas/Money'
++              new_promos:
++                  description: Массив скидок на всю корзину
++                  type: array
++                  items:
++                      $ref: '#/components/schemas/NewPromoForCheckout'

            ItemForCheckout:
                type: object
++              description: Вся информация относится к одному айтему, поэтому надо будет умножать на quantity
                additionalProperties: false
                required:
                - id
                - quantity
                - price
                - options
++              - new_promos
                properties:
                    id:
                        type: string
                    quantity:
                        type: integer
                    price:
++                      description: цена товара до применения всех новых скидок. Для подарочных айтемов из старых скидок, эта цена равна 0.  
                        $ref: '../definitions.yaml#/components/schemas/Money'
                    options:
                        type: array
                        items:
                            $ref: '#/components/schemas/ItemForCheckoutOption'
                    promo_id:
                        type: integer
                        format: int64
++                  new_promos:
++                      description: Массив скидок на данный айтем. Каждая скидка применяется к одному айтему.
++                      type: array
++                      items:
++                          $ref: '#/components/schemas/NewPromoForCheckout'
++                  promo_price:
++                      description: Скидочная цена айтема после применения всех новых скидок. Если новых скидок нет, то поле не придет
++                      $ref: '../definitions.yaml#/components/schemas/Money'


++        NewPromoForCheckout:
++              type: object
++              additionalProperties: false
++              required:
++                - promo_id
++                - amount
++                - discount_provider
++              properties:
++                  promo_id:
++                      type: string
++                  amount:
++                      description: Сумма скидки
++                      type: string
++                      x-taxi-cpp-type: decimal64::Decimal<2>
++                      pattern: '^-?[0-9]+(\.[0-9]{1,2})?$'
++                      example: '"123456.78"'
++                  discount_provider:
++                      description: Кто финансирует акцию
++                      type: string
++                      enum:
++                        - own
++                        - place

```


Стоит обратить внимание, что у подарочных айтемов со старой скидкой price будет приходить нулевой. А в новых скидках будет приходить полная стоимость айтема + в объекте new_promos будет скидка с amount = полная цена айтема
