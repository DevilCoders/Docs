## Экран истории изменения заказа

Задача:


Для [задачи истории изменения заказа](https://st.yandex-team.ru/EDAEATERS-1281) необходимо научиться выдавать информацию по конкретному заказу из истории заказов пользователя для ресторанов и для лавки, как сейчас это сделано для ритейла.

Решение:

В сервисе `eats-orders-info` заведена ручка `/eats/v1/orders-info/v1/get-order`, которая по `order_nr' и 'place_business` может отдать актуальную информацию по заказу.

Эта ручка будет проксировать заказы с ритейла, полученные по ручке `/eats/v1/retail-order-history/customer/order/history` сервиса `eats-retail-order-history`, и коры, поулченные с `/api/v1/orders/{order_nr}`, в перспективе также заказы с лавки. 
Основой АПИ ручки будет АПИ `/eats/v1/retail-order-history/customer/order/history`, дополнительные поля: информация по фидбекам с `eats-feedbacks` и чеки с сервиса `eats-receipts`. 

Кроме того, существует потребность в добавлении информации по service fee и потребность в динамичном заполнении слоя "Доставка и оплата", поэтому часть схемы, отвечающая за доставку и оплату будет вынесена в отдельный объект с массивом. 

Изменения схемы объекта ответа АПИ по сравнению с ручкой `eats-retail-order-history`:
1. Добавление обязательных полей: способа оплаты, чеков; опциональных полей: данные по фидбекам, кэшбэк баллами плюса.
```
    OrderHistoryResponse:
            type: object
            additionalProperties: false
            required:
              - order_nr
              - created_at
                ...
              - original_items
              - diff
+             - receipts
+             - payment_method
            properties:
                donation:
                    $ref: '../definitions.yaml#/components/schemas/DonationInfo'
                order_nr:
                    type: string
                    description: Номер заказа в Еде
                ...
                diff:
                    description: Изменения в составе заказа
                    $ref: "#/components/schemas/OrderDiff"
+               feedback_status:
+                   type: string
+                   description: Статус фидбэка по заказу
+               has_feedback:
+                   type: boolean
+                   description: Флаг наличия фидбэка по заказу
+               receipts:
+                   description: Чеки по заказу
+                   $ref: '../definitions.yaml#/components/schemas/Receipts'
+              payment_method:
+                   description: Тип оплаты
+                   $ref: '#/components/schemas/PaymentMethod'
+               card_system:
+                   description: Тип платежной системы карты
+                   $ref: '#/components/schemas/CardSystem'
+              plus_cashback:
+                 description: Баллы плюса списанные/начисленные
+                 $ref: '#/components/schemas/PlusCashback'
    schemas:
+        Receipts:
+            type: array
+            items:
+                $ref: '#/components/schemas/Receipt'
+
+       Receipt:
+            type: object
+            additionalProperties: false
+            required:
+              - type
+              - receipt_url
+              - mock_name
+            properties:
+              type:
+                description: Тип чека
+                type: string
+                enum:
+                  - payment
+                  - refund
+              receipt_url:
+                description: URL чека
+                type: string
+              created_at:
+                description: Дата и время создания чека
+                type: string
+                format: date-time
+              value:
+                description: Величина суммы из чека
+                $ref: "#/components/schemas/Money"
+              mock_name:
+                description: Текстовая заглушка имени чека на случай отсутствия величины суммы (или пока нет величины)
+                type: string
+
+        PaymentMethod:
+            type: string
+            description: Тип оплаты
+            example: "corp"
+            enum:
+              - card
+              - applepay
+              - googlepay
+              - corp
+              - personal_wallet
+              - badge
+              - cash
+              - coop_account
+              - prepaid
+
+        CardSystem:
+            type: string
+            description: Тип платежной системы карты
+            enum:
+              - RuPay
+              - Maestro
+              - Mastercard
+              - MIR
+              - Visa
+       
+       PlusCashback:
+           type: object
+           description: |
+               Величина начисленных/списанных баллов кэшбека (вид настраивается из конфига
+               EATS_PLUS_ROUNDING_AND_PRECISION_BY_CURRENCY_V2 в зависимости от валюты)
+           additionalProperties: false
+           properties:
+             income:
+               description: Начисление
+               type: string
+             outcome:
+               description: Списание
+               type: string
```
2. Удаление опциональных полей по информаци по доставке и оплате:
```
-                delivery_cost_for_customer:
-                    description: Стоимость доставки (за вычетом возвращённой суммы)
-                    $ref: '#/components/schemas/Money'
-                picking_cost_for_customer:
-                    description: Стоимость сборки (за вычетом возвращённой суммы)
-                    $ref: '#/components/schemas/Money'
-                tips:
-                    description: Чаевые курьеру
-                    $ref: '#/components/schemas/Money'
-                restaurant_tips:
-                    description: Чаевые ресторану
-                    $ref: '#/components/schemas/Money'
        
```
Необходимые данные по оплате будут приходить в формате PaymentDetail:
```
OrderHistoryResponse:
      type: object
      additionalProperties: false
      required:
        - order_nr
        - created_at
+       - payment_details
        - final_cost_for_customer
        - original_cost_for_customer
        - currency
        - status_for_customer
        ...
      properties:
        donation:
          $ref: '../definitions.yaml#/components/schemas/DonationInfo'
        ...
+        payment_details:
+         description: Информация по оплате заказа и дополнительных услуг
+         $ref: '#/components/schemas/PaymentDetails'
    schemas:
+        PaymentDetails:
+          type: object
+          additionalProperties: false
+          required:
+            - payload
+          properties:
+            title:
+              type: string
+              description: Заголовок слоя с информацией по оплате и оплате дополнительных услуг
+            payload:
+              type: array
+              description:
+              items:
+                $ref: "#/components/schemas/PaymentDetail"
+    
+        PaymentDetail:
+          type: object
+          additionalProperties: false
+          required:
+            - title
+            - amount
+          properties:
+            title:
+              description: Заголовок позиции оплаты по услуге
+              type: string
+            subtitle:
+              description: Комментарий позиции оплаты по услуге
+              type: string
+            amount:
+              description: Величина стоимости услуги
+              type: object
+              properties:
+                amount:
+                  $ref: "#/components/schemas/Money"
```

Таким образом, можно будет генерировать слой "Доставка и оплата" на бекенде, что ускорит цикл разработки и позволит гибко добавлять статичную инфромацию по данной теме.
Совместимость будет достигнута тем, что для приложений старых типов, поддерживающий только ручку ритейла, будут продолжаться походы на экран, сгенерированный по старому методу. Новые приложения будут видеть экран, сгенерированный новым методом, заполненный данными с ручки сервиса `eats-orders-info`.

Пример json `PaymentDetail`:
```
{
  "payment_details": {
    "title": "Доставка и оплата",
    "payload": [
      {
        "title": "Стоимость товаров",
        "amount": "2780"
      },
      {
        "title": "Скидка 20%",
        "subtitle": "по промокоду SOSORRY",
        "amount": "-1345"
      }
    ]
  }
}
```
3. Общие изменения: 
3.1. Удаление `place_id` из `Place` и `brand_id` из `Brand`:
```
        Place:
            type: object
            additionalProperties: false
            required:
-             - id
              - slug
              - name
              - business
              - is_marketplace
              - address
            properties:
-               id:
-                   type: string
-                   description: Идентификатор заведения
                slug:
                    type: string
                    description: Человекочитаемый идентификатор заведения.
         ...
         Brand:
            type: object
            additionalProperties: false
            required:
-             - id
              - slug
              - name
            properties:
-               id:
-                   type: integer
-                   format: int64
-                   description: идентификатор бренда заведения
                slug:
                    type: string
```
3.2. Вместо структуры `Currency` будет использоваться новая общепринятая `CurrencyRules`:
```
-        Currency:
-            type: object
-            additionalProperties: false
-            properties:
-                code:
-                    type: string
-                    description: Код валюты (ОКВ)
-                    example: RUB
-                sign:
-                    type: string
-                    description: Знак валюты
-                    example: ₽
-            required:
-              - code

+        CurrencyRules:
+            type: object
+            description: Валюта заказа и правила отображения цены
+            required:
+              - code
+              - sign
+              - template
+              - text
+            properties:
+              code:
+                type: string
+                description: Код валюты
+                minLength: 3
+                maxLength: 3
+                example: "RUB"
+              sign:
+                type: string
+                description: Знак валюты
+                example: "₽"
+              template:
+                type: string
+                description: Шаблон для цен
+                example: "$VALUE$ $SIGN$$CURRENCY$" 
+              text:
+                type: string
+                description: Валюта текстом
+                example: "руб"
```
3.3. У `Money` 2 точки после запятой вместо 4 для удобства просмотра итером:
```
        Money:
-            description: Decimal(18, 4)
+            description: Decimal(18, 2)
             type: string
-            example: '12.5000'
-            x-taxi-cpp-type: decimal64::Decimal<4>
-            pattern: '^-?[0-9]+(\.[0-9]{1,4})?$'
+            example: '12.50'
+            x-taxi-cpp-type: decimal64::Decimal<2>
+            pattern: '^-?[0-9]+(\.[0-9]{1,2})?$'
```
3.4. Обновление объекта `Place`: перенос `Brand` из корня ответа в `Place` и добавление флага `enabled`:
```
Place:
      type: object
      additionalProperties: false
      required:
        - slug
        - name
        - business
        - is_marketplace
        - address
      properties:
        slug:
          type: string
          description: Человекочитаемый идентификатор заведения.
        name:
          type: string
          description: Имя заведения
        business:
          $ref: '#/components/schemas/PlaceBusiness'
        is_marketplace:
          type: boolean
        address:
          $ref: '#/components/schemas/PlaceAddress'
+       brand:
+         $ref: '#/components/schemas/Brand'
+       enabled:
+         type: bool
+         description: Флаг, сигнализирующий, закрыт ли плейс
```
