## Добавление в информацию о позиции в корзине типа каталога (catalog_type) и универсального для всех типов идентификатора (origin_id)
### Проблема
Сейчас есть идентификатор товара в меню ресторана (`place_menu_item_id`), у него тип `int` и он обязательный при получении данных из коры через `stq`.
Но ордер может содержать товары из каталогов, в которых нет `place_menu_item_id` и тип идентификатора не `int`.

Актуальная схема аргументов stq `eats_ordershistory_add_order`:

	arguments:
	   - name: order
         schema:
            type: object
            additionalProperties: false
            description: объект заказа
            required:
                - eats_user_id
                - place_id
                - order_source
                - delivery_location
                - total_amount
                - is_asap
                - created_at
            properties:
                eats_user_id:
                    description: идентификатор итера
                    type: integer
                    format: int32
                taxi_user_id:
                    description: идентификатор пользователя такси
                    type: string
                yandex_uid:
                    description: пасспортный идентификатор
                    type: string
                order_source:
                    description: источник заказа
                    type: string
                    enum:
                        - eda
                        - lavka
                        - pharmacy
                place_id:
                    description: идентификатор ресторана
                    type: integer
                    format: int32
                total_amount:
                    description: суммарная стоимость
                    type: string
                is_asap:
                    description: признак того, что заказ нужно привести к конкретному
                      времени
                    type: boolean
                cancel_reason:
                    description: код причины отмены заказа
                    type: string
                created_at:
                    description: время создания заказа
                    type: string
                    format: date-time
                    example: "2020-04-28T12:00:00+03:00"
                delivered_at:
                    description: время вручения заказа клиенту
                    type: string
                    format: date-time
                    example: "2020-04-28T12:00:00+03:00"
                delivery_location:
                    type: object
                    additionalProperties: false
                    description: объект для хранения гео-координат и адреса места получения заказа
                    required:
                        - lon
                        - lat
                    properties:
                        lat:
                            description: latitude
                            type: number
                            minimum: -90
                            maximum: 90
                        lon:
                            description: longtitude
                            type: number
                            minimum: -180
                            maximum: 180
                        full_address:
                            description: адрес
                            type: string
                            example: "Россия, Москва, Садовническая ул, 81к1"
                        entrance:
                            description: номер подъезда
                            type: string
                        floor_number:
                            description: этаж
                            type: string
                        office:
                            description: квартира
                            type: string
                        doorcode:
                            description: код домофона
                            type: string
                        comment:
                            description: комментарий
                            type: string
                cart:
                    description: коллекция заказанных пользователем товаров
                    type: array
                    items:
                        type: object
                        additionalProperties: false
                        description: товарная позиция в корзине пользователя
                        required:
                            - place_menu_item_id
                            - name
                            - quantity
                        properties:
                            place_menu_item_id:
                                description: идентификатор товара в меню ресторана
                                type: integer
                                format: int32
                            product_id:
                                description: идентификатор товара
                                type: string
                            name:
                                description: название товара, например «картошка»
                                type: string
                            quantity:
                                description: количество товаров в рамках этой позиции
                                type: integer
                                format: int32

### Решение
Расширить `api`, `stq` и таблицу `cart_items` в базе `eats_ordershistory` полями `catalog_type` и `origin_id` и сделать `place_menu_item_id` необязательным

	catalog_type:
	  description: Тип каталога
	  type: string
	  enum:
	     - core_catalog
	     - lavka_catalog
	     - eats-nomeclature
	     - eats-restaurant-nomeclature

	origin_id:
      description: |
	     Универсальный идентификатор внутри каталогов 
	     (тип каталога в catalog_type)
	  type: string

Скопировать имеющиеся значения `place_menu_item_id` в `origin_id` и заполнить `catalog_type` значением `core_catalog`
