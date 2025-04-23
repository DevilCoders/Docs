# Догоняющий кешбэк

## Сегмент пользователей
Не плюсовики.

## Цель
Увеличить ежедневное кол-во Плюсовиков.

## Содержание:
- Промоплашка на самари - при выборе тарифа пользователю будет показываться нотификация под тарифами "мог бы получить столько баллов с подпиской Плюс за этот тариф"
- Шильдик про догоняющий кешбэк - юзер покупает подписку через шильдик во время или в конце поездки и получает за эту поездку баллы.

## Промоплашка под саммари

### Продуктовые требование
1. Должна быть промоплашка под самари, которая информирует пользователя о количестве баллов, которые он получит за поездку, которая сейчас выбрана, с подпиской плюс.
2. Регулирование частоты показа для пользователей 
3. Возможно регулирование по тарифу, цене за поездку

### Пример как выглядит промоплашка

Должна быть надпись что-то следующего: "Ты бы мог получить X баллов кешбэком, если бы у тебя была подписка Яндекс.Плюс."

<img src="https://jing.yandex-team.ru/files/arteeemik/Промоплашка_под_саммари.png" alt="summary" width="200" height="400">

### Как это реализовать
1. Добавляем кол-во кешбэка, которое может получить не плюсовик, если подключит плюс, в преобразования цены по эксперименту. То есть нужно будет добавить поле `possible_cashback_rate` (рейт кешбэка) и `possible_cashback` (сам вычисленный кешбэк с помощью рейта) во все преобразования, в которых мы даем сейчас кешбэк за подписку Плюс. [2 дня]
2. Есть два типа проплашек: 
   - статистические, конфигурируются через админку: https://tariff-editor.taxi.yandex-team.ru/promotions (Промо в селекторе тарифа). Не подходят под эту задачу, так как тексты в этих промоплашках статичные.
   - динамические - генерация промки внешними сервисами, то что нужно в этой задаче. Так как кол-во кешбэка для каждого тарифа меняется.
3. Нужно из `uroutestats` сделать запрос в `tariffs-promotions`, чтобы сохранить кешбэк для не плюсовика по оферу в хранилеще `tariffs-promotions` (redis). Запрос уже есть, нужно будет данные по кешбэку добавить в запрос. [2 дня]
4. В `tariffs-promotions` нужно будет получить и сохранить баллы для промоплашки. [2 дня]
5. Формировать промоплашку из оффера в `tariffs-promotions`. Нужно будет сделать аналогично вот этому тикету: https://st.yandex-team.ru/TAXIBACKEND-33643 . Там также можно будет управлять кол-вом показов и частотой через локальный редис. А также ценой и прочими штуками через эксп. [4-5 дней]
6. inapp будет ходить в tariffs-promotions за промоплашками. Кажется здесь можно правок не делать и там уже есть все, что нужно. 


## Шильдик и банер во время и в конце поездки

<img src="https://jing.yandex-team.ru/files/arteeemik/Догоняющий%20кешбэк.jpg" alt="summary" width="500" height="200">

### Продуктовые требование
1. В процессе/конце поездки нужно пользователю показать шильдик с предложением забрать баллы за поездку, если купить подписки сейчас.
2. При нажатии "забрать баллы", пользователю будет показываться банер с информацией о догоняющем кешбэке и с предложением купить подписку.
3. Частота показа ? Регулирование по кол-ву кешбэка (показывать, когда кешбэк больше, чем обычно в классе)

figma: https://www.figma.com/file/zWSt3vNWyrVQPQYX7YI23B/Go-Плюс?node-id=49224%3A260439

### Как это реализовать

#### Преобразования цены
1. Из предыдущей задачи (промоплашки) в преобразованиях цены будет добавляться возможный кешбэк, который пользователь мог бы получить, если у него была подписка Плюс.
2. В преобразованиях можно по тарифам смотреть, сколько возможного кешбэка пользователь мог получить за заказ, и если это число > какого-то числа, то писать в мету рейты возможного кешбэка. Так можно будет регулировать показ догоняющего кешбэка по кол-ву кешбэку потарифно.

#### Current-prices-calculator
1. В current_prices вычисляем новое поле 'possible_cashback' из меты прайсинга с помощью `possible_cashback_rate` или фиксированного значения possible_cashback из меты прайсинга на старте заказа. 

#### 3.0 totw
1. Прокидываем в totw в resourse_id == `plus-totw-info` поле `possible_cashback` из current_prices:
   
```diff

  - id: plus-totw-info
    after:
      - order-core-orderinfo
    resource: plus-internal-v2-totw-info
    validation:
        content-type: application/json
    body#object:
    ...
      - key: current_prices
        value#object:
          - key: user_total_price
            value#xget: /sources/order-core-orderinfo/response/body/private_data/current_prices/user_total_price
          - key: cashback_price
            value#xget:
                path: /sources/order-core-orderinfo/response/body/private_data/current_prices/cashback_price
                default-value:
          - key: discount_cashback
            value#xget:
                path: /sources/order-core-orderinfo/response/body/private_data/current_prices/discount_cashback
                default-value:
+         - key: possible_cashback
+           value#xget:
+               path: /sources/order-core-orderinfo/response/body/private_data/current_prices/possible_cashback
+               default-value:
          - key: kind
            value#xget: /sources/order-core-orderinfo/response/body/private_data/current_prices/kind
...

```

В ответе totw в поле `plus_info` будет возвращаться новое поле `templates` - список из (key: имя_шаблона, value: значение шаблона).

В totw список шаблонов будет возвращаться в следующем виде:
```diff
{
+   "plus_info": {
+         "templates": [
+              {
+                 "key": "$$TOTW_POSSIBLE_CASHBACK_VALUE$$",
+                 "value": "80"
+              },
+              {
+                  "key": "$$TOTW_POSSIBLE_CASHBACK_TEXT$$",
+                  "value": "баллов"
+              },
+              {
+                  "key": "$$CATCHING_UP_CASHBACK_PURCHASE_PARAMETERS$$",
+                  "value": "order_id=1f8e5f4376fb36aeb013a44887afd0bc&event=catching_up_cashback"
+              }
+         ]
+   }

...
}
```

- Шаблон `$$TOTW_POSSIBLE_CASHBACK_VALUE$$` нужен для того, чтобы подставлять число возможного кешбэка в тексты.
- Шаблон `$$TOTW_POSSIBLE_CASHBACK_TEXT$$` нужен для того, чтобы подставлять правильное склонение слова "баллов" в тексты
- Шаблон `$$CATCHING_UP_CASHBACK_PURCHASE_PARAMETERS$$` нужен для того, чтобы подставлять параметры для покупки Плюса из домика в диплинк (action'ы в шильдике). Диплинки для перехода в typed_screen и диплинки для перехода в домик.


Ресурс `plus-totw-info` берет информацию из ручки `/internal/v2/taxiontheway/info` сервиса Plus. Расширение API этой ручки будет следующим:

```diff
CurrentPrices:
        type: object
        additionalProperties: false
        required:
          - user_total_price
          - kind
        properties:
            user_total_price:
                description: сумма, которую платит пользователь
                type: number
            cashback_price:
                description: сумма услуги кешбека
                type: number
            discount_cashback:
                description: сумма маркетингового кэшбэка
                type: number
            kind:
                type: string
                description: prediction | fixed | taximeter | final_cost
+           possible_cashback:
+               description: сумма возможного кешбэка, который может получить пользователь
+                   при покупке подписки
+               type: number



    TotwResponseObj:
        type: object
        additionalProperties: false
        required:
          - promoted_subscriptions
        properties:
            promoted_subscriptions:
                type: array
                items:
                    $ref: '#/definitions/TotwPromotedSubscriptionV2'
            cost_message_details:
                $ref: '#/definitions/TotwCostMessageDetail'
+           plus_info:
+               $ref: '#/definitions/TotwPlusInfo'
            notifications:
                $ref: '#/definitions/TotwNotification'

+    TotwTemplate:
+        type: object
+        additionalProperties: false
+        description: шаблон - значение для шаблона. Используется клиентами для подстановки значений шаблонов в тексты.
+        required:
+          - key
+          - value
+        properties:
+            key:
+              type: string
+              description: имя шаблона
+              example: "$$TOTW_POSSIBLE_CASHBACK_VALUE$$"
+            value:
+              type: string
+              description: значение для шаблона
+              example: "80"

+    TotwPlusInfo:
+        type: object
+        additionalProperties: false
+        description: Поля для plus_info в totw
+        properties:
+            templates:
+                type: array
+                items:
+                    $ref: '#/definitions/TotwTemplate'
```

Шаблоны могут приходить в текстах или экшенах шильдиков и/или экранов (typed_screens) из ручки sdk-state. Если шаблоны пришли в текстах/экранах, то клиент должен будет их заменить на значения (значения для шаблонов будут приходить в totw). 

Сейчас нужно эту функциональность будет поддержать в следующих типах виджетов: `BUTTON`, `TEXT` и `HORIZONT_TEXT`

#### Дом Плюса

1. Дом плюса должен возвращать шильдик про догоняющий кешбэк. Будет 4 новых шильдика.

В текстах виджетов шильдика будут приходить шаблоны в поле templates. Клиенты должны будут поискать эти шаблоны в текстах виджетов, если нашли их, то попытаться заменить их значениями шаблонов из totw. Если значений для шаблона найдено не было, то виджет нельзя корректно отобразить, и шильдик, в котором находится этот виджет нужно скрыть.

Первый: 
<img src="https://jing.yandex-team.ru/files/arteeemik/Screen%20Shot%202021-07-09%20at%201.47.42%20PM.png" alt="summary" width="200" height="200">

Он показывается следующим пользователям:
- Нет баллов на кошельке (проверяется Домом Плюса)
- Нет подписки (проверяется Домом Плюса)
Называться он будет `plaque:taxi:catching_up_cashback_no_positive_balance`.

Второй (отличие от первого в плане дизайна только в знаке "+": 
<img src="https://jing.yandex-team.ru/files/arteeemik/Screen%20Shot%202021-07-09%20at%201.48.47%20PM.png" alt="summary" width="200" height="200">
Он показывается следующим пользователям:
- Есть баллы на кошельке (проверяется Домом Плюса)
- Нет подписки (проверяется Домом Плюса)
Называться он будет `plaque:taxi:catching_up_cashback_has_positive_balance`.
  

1-й и 2-й шильдик взаимоисключающие, они никогда не должны будут с бека приходить оба сразу.

После того, как пользователь воспользовался догоняющим кешбэком (купил через шильдик и банер про догоняюший кешбэк подписку) и статус покупки подписки стал успешен, клиент должен будет отобразить 3-й или 4-й шильдик:
<img src="https://jing.yandex-team.ru/files/arteeemik/Screen%20Shot%202021-07-09%20at%201.44.43%20PM.png" alt="summary" width="200" height="200">
3-й и 4-й шильдики взаимоисключающие - они никогда не должны будут с бека приходить оба сразу.
3-й шильдик:
- Нет баллов на балансе пользователя (проверяется Домом Плюса).
- Показываться должен только после того, как пользователь успешно купил подписку через банер догоняющего кешбэка подписку. Логика такая: Пользователь купил подписку, если успех, то клиент передергивает sdk-state и этот шильдик возвращается на клиенты. Бек возвращает этот шильдик.
Называться он будет: `plaque:taxi:catching_up_cashback_no_positive_balance_success_purchase`.

4-й шильдик:
- Есть баллы на балансе пользователя (проверяется Домом Плюса).
- Показываться должен только после того, как пользователь успешно купил подписку через банер догоняющего кешбэка подписку. Логика такая: Пользователь купил подписку, если успех, то клиент передергивает sdk-state и этот шильдик возвращается на клиенты. Бек возвращает этот шильдик.
Называться он будет: `plaque:taxi:catching_up_cashback_has_positive_balance_success_purchase`.


А теперь о тех правках в API, которые потребуется сделать, чтобы поддержать шильдик
Будет добавлен один новый виджет (HORIZONT_TEXT) и дополнен существующий виджет (TEXT)
TEXT - В виджет такого типа добавится новое поле опциональное `attributed_text`. Если оно пришло, клиент должен использовать его. Если оно не пришло, то использует поле `text`.
HORIZONT_TEXT - виджет, чтобы можно было отобразить в одну линию текст слева и текст справа кастомный.

Также для виджетов будет возвращаться список шаблонов (опциональное поле `templates`). Это те шаблоны, которые клиентам нужно будет проверить в текстах виджетов, и если они там есть заменить их на значения этих шаблонов из totw. Если шаблон из totw не пришел, то шильдик, в котором состоит этот виджет показаться не должен.

```diff
Widget:
    type: object
    description: Описание виджета - составной части шильдика.
    additionalProperties: false
    required:
      - widget_id
      - type
    properties:
        widget_id:
            $ref: '#/components/schemas/WidgetId'
        type:
            type: string
            description: |
                Тип виджета - определяет его внешний вид.
                Описание конкертного типа располагается в поле,
                соответствующем названию типа (например, `button` для
                типа `BUTTON`).
            enum:
              - BUTTON
              - SWITCH
              - BALANCE_CHANGE
              - BALANCE
              - TEXT
+             - HORIZONT_TEXT
        button:
            $ref: '#/components/schemas/ButtonWidget'
        switch:
            $ref: '#/components/schemas/SwitchWidget'
        balance_change:
            $ref: '#/components/schemas/BalanceChangeWidget'
        balance:
            $ref: '#/components/schemas/BalanceWidget'
        text:
            $ref: '#/components/schemas/TextWidget'
+       horizont_text:
+           $ref: '#/components/schemas/HorizontTextWidget'
        # Тот самый action с диплинком. Если не придет, то виджет - обычный текст
        action:
            $ref: 'actions.yaml#/components/schemas/Action'
+       templates:
+           type: array
+           items:
+              type: string

TextWidget:
   type: object
   description: Виджет - текст.
   additionalProperties: false
   required:
     - text
   properties:
       text:
           $ref: '#/components/schemas/AttributedText'
           example: "Баллы сгорят через 7 дней
+       attributed_text:
+           $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
+           description: Если пришло поле attributed_text, то клиенты должны это поле использовать. attributed_text > text по приоритету.
            

+HorizontTextWidget:
+   type: object
+   description: горизонтальный виджет из двух текстов.
+   additionalProperties: false
+   required:
+     - text_left
+     - text_right
+   properties:
+       text_left:
+           $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
+           example: |
+              items: [
+                  {
+                     "text": "после поездки",
+                     "type": "text"
+                  }
+               ]
+       text_right:
+           $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
+           example: |
+              items: [
+                  {
+                     "text": "+80",
+                     "type": "text"
+                  }
+               ]

``` 
Два виджета над кнопкой:
```diff
{
    // уникальный ID виджета
    "widget_id": "1-й текст над кнопкой",
    // тип виджета - определяет его внешний вид
    "type": "TEXT",
    "text": "+$$TOTW_POSSIBLE_CASHBACK_VALUE$$",
    "attributed_text": [
    {
        "color": "#AABBCC",
        "font_size": 1,
        "font_style": "normal",
        "font_weight": "medium",
        "meta_style": "title-semibold",
        "text": "+$$TOTW_POSSIBLE_CASHBACK_VALUE$$",
        "type": "text",
    }
   ],
   "action": {
      "type": "DEEPLINK",
      "deeplink": "yandextaxi://cashback?plus_context=$$CATCHING_UP_CASHBACK_PURCHASE_PARAMETERS$$"
   },
   templates: [
      "$$TOTW_POSSIBLE_CASHBACK_VALUE$$",
      "$$CATCHING_UP_CASHBACK_PURCHASE_PARAMETERS$$"
   ]
}

{
    // уникальный ID виджета
    "widget_id": "2-й текст над кнопкой",
    // тип виджета - определяет его внешний вид
    "type": "TEXT",
    "text": "$$TOTW_POSSIBLE_CASHBACK_TEXT$$ за эту поездку",
    "attributed_text": [
    {
        "color": "#AABBCC",
        "font_size": 1,
        "font_style": "normal",
        "font_weight": "medium",
        "meta_style": "title-semibold",
        "text": "$$TOTW_POSSIBLE_CASHBACK_TEXT$$ за эту поездку",
        "type": "text",
    }
   ],
   "action": {
      "type": "DEEPLINK",
      "deeplink": "yandextaxi://cashback?plus_context=$$CATCHING_UP_CASHBACK_PURCHASE_PARAMETERS$$"
   },
   templates: [
      "$$TOTW_POSSIBLE_CASHBACK_TEXT$$",
      "$$CATCHING_UP_CASHBACK_PURCHASE_PARAMETERS$$"
   ]
}
```

Кнопка:
```diff
{
    // уникальный ID виджета
    "widget_id": "кнопка для вызова фуллскрина",
    // тип виджета - определяет его внешний вид
    "type": "BUTTON",
    // поле с описанием указанного типа
    "button": {
        "text": "Забрать"
    },
    // действие, производимое при нажатии на виджет
    "action": {
        "type": "DEEPLINK",  // экран будет открываться по диплинку
        "deeplink": "yandextaxi://plus_typed_screen?type=catching_up_cashback&plus_context=$$CATCHING_UP_CASHBACK_PURCHASE_PARAMETERS$$" // Общий диплинк
    },
   templates: [
      "$$CATCHING_UP_CASHBACK_PURCHASE_PARAMETERS$$"
   ]
}
```

1-й и 2-й шильдики по структуре аналогичны:

```diff
"plaque:taxi:catching_up_cashback_has_positive_balance": {
      "condition": {
        "screens": [
          "transporting", // Экран в процессе поездки
          "feedback" // Экран оценки поездки в конце поездки
        ]
      },
      "layout": "VERTICAL",
      "params": {
        "close_after": 60,
        "show_after": 0
      },
      "priority": 50,
      "visibility_requirements": {
        "has_plus": false,
      },
      "widgets": [
        "1-й текст над кнопкой",
        "баллы за эту поездку",
        "кнопка для вызова фуллскрина"
      ]
    }
```

3-й шильдик:
```diff
"plaque:taxi:catching_up_cashback_no_positive_balance_success_purchase": {
      "condition": {
        "screens": [
          "transporting", // Экран в процессе поездки
          "feedback" // Экран оценки поездки в конце поездки
        ]
      },
      "layout": "VERTICAL",
      "params": {
        "close_after": 60,
        "show_after": 0
      },
      "priority": 50,
      "visibility_requirements": {
        "has_plus": true,
      },
      "widgets": [
        "ATTRIBUTED_TEXT",
        "ATTRIBUTED_TEXT"
      ]
    }
```

4-й шильдик:
```diff
"plaque:taxi:catching_up_cashback_has_positive_balance_success_purchase": {
      "condition": {
        "screens": [
          "transporting", // Экран в процессе поездки
          "feedback" // Экран оценки поездки в конце поездки
        ]
      },
      "layout": "VERTICAL",
      "params": {
        "close_after": 60,
        "show_after": 0
      },
      "priority": 50,
      "visibility_requirements": {
        "has_plus": true,
      },
      "widgets": [
        "BALANCE",
        "HORIZONT_ATTRIBUTED_TEXT"
      ]
    }
```

Также нужно понимать, что в банере тоже нужно тексты заменять, для этого в API банеров появятся опциональное поле `templates`: 
```diff
        TypedScreens:
            type: object
            description: Клиентские экраны
            additionalProperties: false
            required:
              - 'items'
            properties:
                'items':
                    type: array
                    items:
                        $ref: '#/components/schemas/TypedScreen'
        TypedScreen:
            type: object
            additionalProperties: false
            properties:
                'type':
                    type: string
                    description: тип экрана
                    example: catching_up_cashback  // новый тип экрана для догоняющего кешбэка
                payload:
                    $ref: '#/components/schemas/ScreenPayload'
+               templates:
+                   type: array
+                   items:
+                       type: string
            required:
              - type
              - payload            
```


2. При открытии typed_screen из этого шильдика и нажатии покупки подписки, в ручку покупки плюса `/4.0/sweet-home/v1/subscriptions/purchase` клиенты должны будут передавать order_id текущего заказа в такси и event (событие, по которому происходит покупка Плюса). 
Параметры `order_id` и `event` будут доступны из параметров deeplink, по которому пользователь попал в typed_screen ("yandextaxi://open_screen_catching_up_cashback?$$CATCHING_UP_CASHBACK_PURCHASE_PARAMETERS$$").
   
Также при нажатии на текст в шильдике про догоняющий кешбэк, для пользователя будет открывать дом Плюса по диплинку, в параметрах которого будет защито поле `plus_context` - query строка из параметров для запроса в ручку покупки Плюса.

```diff
+Request `/4.0/sweet-home/v1/subscriptions/purchase?order_id=1f8e5f4376fb36aeb013a44887afd0bc&event=catching_up_cashback`
{
  "payment_method_id": "card-x82e9d935e2eff30d6ff2956f",
  "subscription_id": "ya_plus_rus_v2_trial",
}

```

Новый экран (банер) добавим после того, как экраны будут поддержаны в горящем шильдике. Он будет из домика возвращаться.

3. Добавляем в дом Плюса stq-таску `plus_sweet_home_purchase_subscriptions_status`, которая будет ставиться из ручки `/4.0/sweet-home/v1/subscriptions/purchase` в самом начале (до похода в ручку медиабиллинговую покупки Плюса) и если event == `catching_up_cashback`. В параметрах stq таски будут `order_id`, `event`, и поле subscription_payload (в нем будет храниться информация из запроса ручки `/4.0/sweet-home/v1/subscriptions/purchase`).

Если stq-таску не удалось поставить, то ручка покупки Плюса вернет ошибку. Если таску удалось поставить, то stq-таска и ручка `/4.0/sweet-home/v1/subscriptions/purchase` сделают запрос в ручку `/subscription/submit-native-order` медиабиллинговую для покупки Плюса и получат из него orderId заказа. stq будет поллить результат покупки по orderId раз в 5-10 секунд. Если ручка вернет статус покупки `ok`, значит подписка точно куплена (дежурный от МБ это подтвердил) и можно запустить процесс начисления баллов.

#### Сервис cashback
1. При успешной покупке Плюса stq-таска `plus_sweet_home_purchase_subscriptions_status` с помощью order_core запишет в order_proc два поля (`is_cashback` == true и `is_possible_cashback` == true). Дальше запустит stq-таску `cashback_rates_processing`. Эта таска проверит рейты кешбэка из меты прайсинга, возьмет рейты из меты прайсинга для возможного кешбэка и зарегистрирует рейты кешбэка в таблице `order_rates` (базы cashback) в поле rates (`possible_cashback_by_classes` - будет лежать рядом с `by_classes`). 

2. Дальше stq-таска `plus_sweet_home_purchase_subscriptions_status` запустит  stq-таску `universal_cashback_processing`, которая обработает начисление баллов. Начисления будем производить через transactions, как для такси заказов.
   
3. Также нужно будет подкорректировать ручку `/v1/cashback/calc`, которая будет рассчитывать абсолютное число кешбэка для таких вот начислений, и stq-таску `cashback_charge_processing`, чтобы производить начисление баллов.

4. Баллы, которые будем начислять - будут маркетинговыми. Почему не агентскими - потому что во время поездки водитель уже знает цену за заказ, и уменьшить её на 10% мы не можем. 

5. Что делать при рефандах/изменениях цены заказа:
      - Учитывая, как сейчас устроены баллы, ucb вызывается при любом изменении стоимости заказа, то есть и догоняющий кешбэк будет тоже изменяться в такой логике.

### Ориентировочные сроки по шильдику/банеру:
1. Добавление новых виджетов и шильдика в доме плюса - 1-1.5 день
2. Current-prices (добавление нового поля possible_cashback) - 0.5-1 день 
3. В totw передавать в plus-totw-info поле current_prices/possible_cashback - 0.2-0.5 дня
4. Правки в ручке `/4.0/sweet-home/v1/subscriptions/purchase` - 2 дня
5. Написание новой stq `plus_sweet_home_purchase_subscriptions_status` - 3-4d
6. Правки в stq `cashback_rates_processing` - 3 дня
7. Правки в `/v1/cashback/calc` - 2 дня
8. Правки в stq `universal_cashback_processing` - 2 дня
9. Правки в stq `cashback_charge_processing` - 3 дня
10. Правки в ручке `/internal/v2/taxiontheway/info` - 2-3 дня

### Что нужно сделать на клиентах
- Поддержать передачу новых параметров в ручку покупки Плюса из диплинка в экран и в дом Плюса через query параметры.
- Научиться работать с templates, которые приходят в виджетах из домика и в typed_screens. А также приходят их значения в totw.
- Научиться открывать общий диплинк для typed_screens(экранов из домика)
- Поддержать два новых виджета ATTRIBUTED_TEXT и HORIZONT_ATTRIBUTED_TEXT
