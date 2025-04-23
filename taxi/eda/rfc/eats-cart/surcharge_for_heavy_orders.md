# Доплата за тяжелые заказы в ритейле

## Проблема
Мы доплачиваем курьерам за то, что они возят/несут тяжелые заказы (например, для пеших - это от 8кг), при этом с пользователя за это денег не берем.
В структуре CPO - это 6 руб по сервису, которые нужно компенсировать.

## Решение
Брать с пользователя деньги за вес, при достижении определенных трэшхолдов. Доплату за тяжелые заказы, на первом этапе, было решено включить в стоимость доплаты за доставку - `delivery_fee`. Позже планируются правки, чтобы отправлялось отдельной статьей.

## Реализация на бэке
Доплата за тяжелые заказы должна проходить через сервис прайсинга (eda-delivery-price). Поэтому логика по расчету доплаты за тяжелый заказ будет находиться на стороне прайсинга. 

## Доработки в корзине (eats-cart)
1. Нужно считать вес корзины `cart_weight` и передавать его в прайсинг, в ручку `/internal/v1/cart-delivery-price-surge` которая отвечает за стоимость доставки и сурж для корзины. Сейчас корзина уже в нее ходит.

   1.1 Для получения веса всей корзины можно использовать логику метода [SumItemWeights](https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/eats-cart/src/builders/cart.cpp?rev=r9151540#L424), который возвращает вес всей корзины.

2. В ответе от прайсинга в объекте [CartDeliveryPrice](https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/eda-delivery-price/docs/yaml/definitions.yaml?rev=r9180849#L895) добавится поле:

    - weight_fee - опциональное поле, размер доплаты за тяжелый заказ. Эта информация нужна для отображения на информере.
      
    2.1 `weight_fee` нужно сохранять в БД в таблицу `extra_fees`.
    
3. Поле `subtitle` объекта `AdditionalPayment` необходимо расширить описанием вида "В том числе ХХХ р за доставку ХХ кг", текст брать из Танкера. Подстрочка появляется в случае, если вес заказа превышает первый трэшхолд веса, за который начинаем брать деньги. При этом вторая строчка меняется - показываем не до бесплатной доставки, а до стоимости за текущий трэшхолд - `weight_fee`.  Если за вес доплату не берем, подстрочка не появляется и отображаем 1 строчку "Закажите еще на XX руб. для бесплатной доставки."

4. Для дополнительного платежа `delivery_fee` структуры `AdditionalPayment` нужно будет сделать доработку в структуре `DetailsForm`. Она появляется при нажатии на кнопку информации о дополнительном сборе. 

5. Необходимо расширить поле `description`, а именно добавить в него информацию по стоимости доставки и доплаты за тяжелый заказ. Текст брать из Танкера. (см. https://wiki.yandex-team.ru/users/abutolin/doplata-za-tjazhjolye-zakazy-v-ritejjle/). Строчки "Стоимость доставки" и "Доплата за вес" по умолчанию есть всегда. В случае, когда доплаты за вес нет или стоимости доставки нет, пишем 0 руб.

## Доработки в прайсинге (eda-delivery-price)
1. На стороне прайсинга будет реализована логика подсчета доплаты за тяжелый заказ (ответственный https://staff.yandex-team.ru/igor-vorobyev).

2. В запросе от корзины в ручку `/internal/v1/cart-delivery-price-surge` добавится поле `cart_weight` - вес всей корзины.

   2.1 В ответе ручки в `CartDeliveryPrice` добавится поле:
   
      - weight_fee - опциональное поле, размер доплаты за тяжелый заказ.
   
   2.2 Во всех расчетах `delivery_fee` в прайсинге нужно учитывать `weight_fee`, так как доплата за тяжелый заказ входит в стоимость доставки, но на корзину возвращать их по отдельности.
    
3. Ответ ручки `/v1/calc-delivery-price-surge`, в которую ходит каталог (eats-catalog), нужно дополнить информацией по трешхолдам для тяжелых заказов. На примере массива [fees](https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/eda-delivery-price/docs/yaml/definitions.yaml?rev=r9180849#L394) который состоит из трешхолдов для стоимости за доставку, нужно передавать массив `weight_fees`.
   
   3.1 `weight_fees` - нужно дополнить объектами `WeightThreshold`. 
   
   3.2 `WeightThreshold` - трешхолд для доплаты за тяжелый заказ. 
   
Это нужно для отображения трешхолдов на фронтах.

Схема `WeightThreshold`:
```
    WeightThreshold:
        type: object
        required:
            - weight_cost
            - weight_threshold
        additionalProperties: false
        properties:
            weight_cost:
                type: number
            weight_threshold:
                type: number
```
## Пример:
```
    {
        weight_cost: 0, // 0р доплата за вес 
        weight_threshold: 8 // до 8 кг доплаты нет 
    },
    {
        weight_cost: 40, // 40р доплата за вес 
        weight_threshold: 15 // до 15 кг 
    }
```

## Доработки в каталоге (eats-catalog)
1. Нужно принимать от прайсинга массив `weight_fees` из `WeightThreshold`(схема выше) - трешхолды по тяжелым заказам.

2. В ответе ручек `/eats-catalog/v1/brand/{brand_slug}` и `v2/catalog/{slug}` в поле [Place](https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/eats-catalog/docs/yaml/api/slug.yaml?rev=r8998583#L619) нужно добавить поле `weight_thresholds`.

```
   WeightThresholds:
      type: array
      description: Содержит информацию необходимую для расчета стоимости доплаты за тяжелый заказ
      items:
          $ref: "#/components/schemas/WeightThreshold"
          
   WeightThreshold:
      type: object
      additionalProperties: false
      required:
        - orderWeight
        - weightCost
        - decimalWeightCost
        - title
      properties:
          orderWeight:
              type: object
              additionalProperties: false
              description: Интервал веса заказа для которого применяется эта доплата
              required:
                - min
                - max
              properties:
                  min:
                      type: string
                  max:
                      type: string
                      nullable: true
          weightCost:
              type: integer
          decimalWeightCost:
              $ref: "../definitions.yaml#/components/schemas/Money"
          title:
              type: string
              description: Заголовок интервала
              example: до 8 кг
```

3. Объект [Message](https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/eats-catalog/docs/yaml/api/slug.yaml?rev=r8998583#L514) нужно будет расширить опциональным полем `description` - описание сообщения.

4. В ответе ручки каталога ручек `/eats-catalog/v1/brand/{brand_slug}` и ``v2/catalog/{slug}``, поле [Messages](https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/eats-catalog/docs/yaml/api/slug.yaml?rev=r8998583#L554) (сообщения, показываемые в боттомшите), расширяем полем `weight_thresholds`. Это нужно для отображения трешхолдов за тяжелые заказы в баттомшите.
   
   4.1 `weight_thresholds` является объектом `Message`, как и остальные трешхолды. 
   
   4.2 У `weight_thresholds` должен быть заголовок. 

5. В объекте `Messages` есть поле `thresholds`, которое представляет собой трешхолды за доставку. Необходимо добавить описание к этому полю. Описание нужно будет брать из Танкера.

6. В объекте `ShippingInfoAction` в поле `deliveryFee` учесть стоимость максимальной доплаты за тяжелый заказ. Это нужно для того, чтобы корректно отображать информацию вида "Доставка 0 - 199", где в 199 должна так же входить доплата за тяжелый заказ.

## Доработки на фронтах
1. Необходимо показывать клиенту информер в котором будет указано сколько составит доплата за тяжелый заказ. Формат информера описан выше.

2. В баттомшите на меню добавить информацию по трешхолдам для тяжелых заказов. Трешхолды (`WeightThresholds`, см выше) будут приходить в ответе ручек `/eats-catalog/v1/brand/{brand_slug}` и `v2/catalog/{slug}`, как и трешхолды для "Стоимости доставки".
