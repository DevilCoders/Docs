## Задача
Нужно уметь настраивать коммуникации и объекты на карте по id подписки Плюса, которая доступна пользователю для покупки.


## Стейкхолдеры
### Клиентская разработка SDK
@vrmaks
@maxost
### inapp-communications
@privet
### Layers
@nknv-roman
@mstepa
### Домик
@rgnlax
@arteeemik

## Решение
В ручках inapp-communications 
- `4.0/inapp-communications/communications`  
  50 RPS
-  `/inapp-communications/v1/promos-on-map`   
  1200 RPS

должен появиться новый кварг для проброса в эксперименты: `available_subscription_id`.

Есть несколько вариантов получить available_subscription_id
### 1. Запросить available_subscription_id из plus-sweet-home
В plus-sweet-home добавляется новая ручка для получения списка доступных подписок по yandex_uid.
inapp-communications получает available_subscription_id из этой ручки.  

> Зелёным цветом обозначены добавления.  
> Миро: https://miro.com/app/board/o9J_l6HWkzE=/ 

![поход в домик](https://jing.yandex-team.ru/files/danielkono/%D0%9A%D0%BE%D0%BC%D0%BC%D1%83%D0%BD%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D0%B8%20%D0%BF%D0%BE%20%D0%B4%D0%BE%D1%81%D1%82%D1%83%D0%BF%D0%BD%D0%BE%D0%B8%CC%86%20%D0%BF%D0%BE%D0%B4%D0%BF%D0%B8%D1%81%D0%BA%D0%B5%20-%20%D0%BF%D0%BE%D1%85%D0%BE%D0%B4%20%D0%B2%20%D0%B4%D0%BE%D0%BC%D0%B8%D0%BA.c8ba085.png)
#### Изменения в API
https://st.yandex-team.ru/TAXIBACKEND-36563

#### Проблемы
Это добавляет + 1.2к RPS в plus-sweet-home и fast-prices/billing-transitions (сервис Медиабиллинга). Неизвестно, готов ли к этому Медиабиллинг.

Проблема с Гео — логика определения региона в Домике может не совпадать с логикой определения региона в inapp-communications и layers

### 2. Проксировать available_subscription_id через клиент
Клиент получает доступные подписки из ручки `4.0/sweet-home/v2/sdk-state` 
После этого он может передать available_subscription_id в ручки  `4.0/inapp-communications/communications` и `4.0/layers/v2/objects`
![проксирование subscription_id](https://jing.yandex-team.ru/files/danielkono/%D0%9A%D0%BE%D0%BC%D0%BC%D1%83%D0%BD%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D0%B8%20%D0%BF%D0%BE%20%D0%B4%D0%BE%D1%81%D1%82%D1%83%D0%BF%D0%BD%D0%BE%D0%B8%CC%86%20%D0%BF%D0%BE%D0%B4%D0%BF%D0%B8%D1%81%D0%BA%D0%B5%20-%20%D0%BF%D1%80%D0%BE%D0%B1%D1%80%D0%BE%D1%81%20id.6315eaf.png)
#### Изменения в API 
`4.0/inapp-communications/communications`
```diff
    CommunicationsRequest:
        type: object
        additionalProperties: false
        properties:
            ...
+           plus_subscription_info:
+               type: object
+               additionalProperties: false
+               properties:
+                   available_subscription_id:
+                       type: string
```

`4.0/layers/v2/objects`
```diff
    ObjectsV2Request:
        type: object
        additionalProperties: false
        properties:
            state:
                description: текущее состояние приложения
                $ref: "#/definitions/State"
            ...

    State:
        type: object
        description: Состояние приложения для внешней ручки
        additionalProperties: false
        properties:
             ...
+            user:
+               type: object
+               description: Дополнительный контекст о юзере
+               additionalProperties: false
+               properties:
+                    plus_subscription_info:
+                        type: object
+                        additionalProperties: false
+                        properties:
+                            available_subscription_id:
+                                type: string
              ...
```
`/inapp-communications/v1/promos-on-map`
```diff
    PromosRequest:
        type: object
        additionalProperties: false
        properties:
            ...
+           plus_subscription_info:
+           type: object
+           additionalProperties: false
+           properties:
+               available_subscription_id:
+               type: string
```

Клиент получает subscription_id из ручки `4.0/sweet-home/v2/sdk-state` и явно передаёт в `4.0/inapp-communications/communications` и `4.0/layers/v2/objects`

#### Проблемы
- inapp-communications/communications и layers/v2/objects будут зависеть от ответа sdk-state.
- после покупки подписки клиент должен перезапросить коммуникации

### 3. Проксировать список key-value
Теоретически, в будущем нам может потребоваться какой-то ещё контекст из домика в коммуникациях кроме доступной подписки, и мы не сможем получить его back2back.  
Тогда будет удобно, если клиент будет получать непрозрачный для него список key-value с дополнительным контекстом из `sdk-state` и передавать его в ручки `4.0/inapp-communications/communications` и `4.0/layers/v2/objects` в поле `plus_subscription_info`.

Тогда мы сможем добавить новую информацию в контекст без релиза клиента.
![проброс непрозрачной структуры](https://jing.yandex-team.ru/files/danielkono/%D0%9A%D0%BE%D0%BC%D0%BC%D1%83%D0%BD%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D0%B8%20%D0%BF%D0%BE%20%D0%B4%D0%BE%D1%81%D1%82%D1%83%D0%BF%D0%BD%D0%BE%D0%B8%CC%86%20%D0%BF%D0%BE%D0%B4%D0%BF%D0%B8%D1%81%D0%BA%D0%B5%20-%20%D0%BF%D1%80%D0%BE%D0%B1%D1%80%D0%BE%D1%81%20%D0%BD%D0%B5%D0%BF%D1%80%D0%BE%D0%B7%D1%80%D0%B0%D1%87%D0%BD%D0%BE%D0%B8%CC%86%20%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D1%8B.2ecade6.png)
### Изменения в API
Изменения в API аналогичны предыдущему варианту, кроме них в ответ `sdk-state` добавляется новое поле `communications_subscription_info`
```diff
Subscription:
            type: object
            description: Информация о подписке пользователя.
            additionalProperties: false
            required:
              - status
            properties:
                ...
+               communications_subscription_info:
+                   type: object
+                   additionalProperties: 
+                       type:
+                           $oneOf:
+                             - string
+                             - number
+                             - boolean
+                   properties:
+                       available_subscription_id:
+                           type: string
```
