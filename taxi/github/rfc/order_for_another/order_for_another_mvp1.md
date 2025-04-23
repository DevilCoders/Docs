# Заказ другому 2.0

## Бизнес-задача

В рамках проекта по [новому семейному аккаунту ](https://st.yandex-team.ru/TAXIPROJECTS-2387) необходимо переработать UI
заказа другому, т.к. это одна из основных вещей, которая ассоциируется у клиентов с семейностью. В качестве первого
этапа планируется реализовать следующий функционал:

* Новое модельное окно заказа другому

![image](static/modal_window.png)

* Выбор контактов

![image](static/new_contact_selections.png)

* Промотирующий виджет

![image](static/promo_widget_1.png)

![image](static/promo_widget_2.png)

## Техническая реализация

### Модальное окно заказа

* из ручки protocol/launch приходит ключ `order_for_another_init_distance_meters`, в котором содержится расстояние от
  пользователя, при котором надо показывать окно вызова другому
* в момент нажатия кнопки `Заказать` в случае, если расстояние между пользователем и точкой заказа >= значения параметра
  из пункта выше пользовать видит предложение заказа другому

Такой протокол обеспечивается экспериментом [order_for_another](https://tariff-editor.taxi.tst.yandex-team.ru/experiments3/experiments/show/order_for_another/) в `/launch`. При этом клиент сразу получает локализованные ключи. 

На рисунке ниже показано соотношение ключей с элементами на экране.

![image](static/modal_order_for_another.jpg)

### Промотирующий виджет

В ручку `/taxiontheway` добавляется поле `promoblocks`, которое расширяет структуру [inapp-communications](https://github.yandex-team.ru/taxi/uservices/blob/develop/services/inapp-communications/docs/yaml/definitions.yaml#L1467) и отображает промоблок на экране заказа. При этом поле `configuration` может отсутствовать, что означает дефолтное применение `configuration.type` - `list`.

![image](static/promo_widget_2.png)

```yaml
promoblocks:
    type: object
    properties:
        items:
            type: array
            items:
                $ref: 'PromoblockItem'
    additionalProperties: false
    required:
      - items

PromoblockItem:
        type: object
        properties:
            id:
                type: string
            meta_type:
                description: |
                    Поле для внутренней работы блендера. Игнорируется клиентами.
                    inapp-communications также агрегирует внутри себя все промоблоки
                    всех других источников и передаёт их клиентам.
                type: string
            title:
                type: object
                properties:
                    items:
                        $ref: '#/definitions/PromoblockContentArray'
                additionalProperties: false
                required:
                  - items
            text:
                type: object
                properties:
                    items:
                        $ref: '#/definitions/PromoblockContentArray'
                additionalProperties: false
                required:
                  - items
            icon:
                type: object
                properties:
                    image_tag:
                        type: string
                    image_url:
                        type: string
                additionalProperties: false
            widgets:
                type: object
                properties:
                    deeplink_arrow_button:
                        type: object
                        description: |
                            См. пример https://jing.yandex-team.ru/files/ihelos/2020-07-08%2009.13.40.jpg
                            Данный тип виджетов поддерживает переход по диплинкам с нажатием на стрелочку.
                        properties:
                            deeplink:
                                type: string
                            color:
                                type: string
                            items:
                                $ref: '#/definitions/PromoblockContentArray'
                        additionalProperties: false
                        required:
                          - deeplink
                          - color
                          - items
                additionalProperties: false
            configuration:
                type: object
                description: |
                    Настраивает промоблок для отображения на клиенте.
                properties:
                    type: 
                        type: string
                        description: способ отрисовки промоблока на клиенте. Для list смотри static/promo_widget_2.png
                        enum:
                           - list
                           - bubble
                additionalProperties: false
        additionalProperties: false
        required:
          - id
          - meta_type
          - title
          - widgets
```


Сервис inapp-communications будет понимать, надо ли отдать клиенту этот виджет на основании наличия
поля `extra_contact_phone`, которое будет прокидываться сервисом api-proxy при формировании ответа на totw.

