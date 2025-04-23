# Вынос чекеров из коры и новые скидки в internal ручках

## Чекеры

Чекеры - это набор проверок, которые происходят перед созданием заказа. Сейчас все чекеры находятся в коре.
Среди этих чекеров есть "чекер актуализации скидок". Он вычисляет скидки на текущую корзину пользователя и далее сравнивает их с уже примененными. Если они совпадают, то все ок. Иначе возвращается ошибка.

## Новые скидки в internal ручках

Сейчас в некоторых internal ручках мы передаем данные о промоакциях. Т.к в скором времени мы переедем на новый сервис скидок eats-discounts, необходимо сделать так, чтобы при передаче информации о скидках, которых нет в коре, мы не ловили ошибки, а чекер актуализации скидок отрабатывал на стороне eats-cart

## Задача

1. Продумать, как правильно постепенно переносить все чекеры из коры в eats-cart
1. Продумать, как правильно перенести и работать с чекером актуализации скидок. Т.к в новой корзине появляются новые скидки из eats-discounts, то информации о них в коре нет, поэтому необходимо как-то поддержать.

## Решение

## Плавный перенос чекеров
Для начала необходимо каждому из чекеров дать свой уникальный идентификатор. Предлагаю сделать его строковым, чтобы легче было понимать, например, "checker_updated_discounts".

Перед тем как запустить чекеры, кора получает информацию о корзине из ручек `/internal/eats-cart/v1/lock_cart_pickup` или `/internal/eats-cart/v1/lock_cart`. Я предлагаю запускать чекеры на стороне eats-cart в этих ручках.
И если какой-то чекер на стороне eats-cart не выполнится, то эти ручки вернут Response400, а именно:
```
'400':
    description: Ошибка
    content:
        application/json:
            schema:
                $ref: '../definitions.yaml#/components/schemas/CheckerError'

        CheckerError:
            type: object
            additionalProperties: true
            x-taxi-additional-properties-true-reason: allOf
            allOf:
              - $ref: '#/components/schemas/BaseError'
              - $ref: '#/components/schemas/PayloadObject'

        PayloadObject:
            type: object
            additionalProperties: true
            x-taxi-additional-properties-true-reason: allOf
            properties:
                payload:
                    type: object
                    additionalProperties: true
                    x-taxi-additional-properties-true-reason: Arbitrary faulty parameters
                        are possible

        BaseError:
            type: object
            additionalProperties: true
            x-taxi-additional-properties-true-reason: allOf
            required:
              - domain
              - code
              - err
            properties:
                domain:
                    description: UserData or Network
                    type: string
                code:
                    type: integer
                err:
                    description: Текст ошибки
                    type: string

```
Такой 400 ответ кора будет обрабатывать и если он придет, то прокидывать дальше клиенту.

Также в АПИ этих ручек надо добавить required поле applied_checkers:
```
applied_checkers:
    items:
        type: array
        items:
            type: string
``` 
Поле applied_checkers - это список чекеров, которые запускались в eats-cart.

И тогда новым условием успешного прохождения чекера в коре становится `"название чекера есть в applied_checkers" ИЛИ "чекер отработал успешно""`. 

Таким образом чтобы полностью перенести чекер в eats-cart нужно будет написать его логику в eats-cart и выкатить. Старый чекер в коре сам перестанет выполнятся, и данный чекер можно будет выпиливать из коры по возможности.

## Новые скидки в intenal ручках

См. файл new_discounts.md


Информацию о скидках мы передаем в 4 internal ручки: `/internal/eats-cart/v1/create_cart`, `/internal/eats-cart/v1/get_cart`, `/internal/eats-cart/v1/lock_cart_pickup`, `/internal/eats-cart/v1/lock_cart`. В ручках lock они нужны для чекеров, в ручке create_cart и get_cart они нужны для информации. 


Также из ручки lock_cart берутся данные для ревизии заказов. Т.к информации о новых скидках в коре нет, то необходимо дополнительно ее прокидовать из eats-cart.

Предлагаю в ответ lock_cart(_pickup) добавить новое поле new_promos, в котором будет хранится инфа о скидках, которых нет в коре.
```
new_promos:
    type: array
    items:
        $ref: '#/components/schemas/NewPromoForCheckout'

NewPromoForCheckout:
    type: object
    additionalProperties: false
    required:
      - amount
      - discount_type
      - discount_provider
      - quantity
    properties:
        item_id:
            type: string
        amount:
            description: Сумма скидки
            type: string
            x-taxi-cpp-type: decimal64::Decimal<2>
            pattern: '^-?[0-9]+(\.[0-9]{1,2})?$'
            example: '"123456.78"'
        discount_type:
            description: Тип скидки для доп логики в checkout 
            type: string
        discount_provider:
            description: Кто финансирует акцию
            type: string
            enum:
              - own
              - place
        quantity:
            type: integer
```

По этим данным мы сможем добавить в ревизию информацию о скидках.


Таким образом ничего страшного в том, что мы передадим информацию о скидках, которых нет в коре в create_cart и get_cart - нет. А для лок ручек - мы напишем чекер актуализаций у себя в корзине для корзин ритейла и будем заполнять поле applied_checkers, а также начнем передавать информацию о новых скидках в поле new_promos. Поэтому для ритейла, где мы как раз и внедряем наши акции, чекер запускаться не будет, а для ресторанов - будет. Также информация о информация о новых скидках будет добавляться в ревизию.

## Tickets
1. https://st.yandex-team.ru/EDADEV-43884 - Team A
2. https://st.yandex-team.ru/EDADEV-43885 - ОПГ
3. https://st.yandex-team.ru/EDAJAM-46 - JamTeam
