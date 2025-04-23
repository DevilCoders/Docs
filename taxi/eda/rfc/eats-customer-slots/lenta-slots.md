# Подключаем партнера со своими слотами сборки (Лента)

## Архитектура
![Архитектура](images/Lenta.png)

## Диаграмма вызовов
![Диаграмма вызовов](images/Lenta_Order_Flow.png)


## Описание предлагаемого Решения

Мы хотим подключить слоты Ленты, а именно:
- показывать покупателю слоты доставки, основанные на слотах сборки ленты
- принимать заказы в эти слоты
- назначать курьера к концу слота сборки


### Тикеты по фиче:
* Архитектура и диаграммы вызовов: https://st.yandex-team.ru/RETAILSPECS-68
* Эпик по слотам и исполнению заказа: https://st.yandex-team.ru/RETAILDEV-937
* Интеграция с Лентой: https://st.yandex-team.ru/EDAPRODUCT-2106

### Что делаем

#### Каталог:
* eats-catalog-storage должен начать отдавать place_origin_id из ручки https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Uservices/eats-catalog-storage/api/place/#internaleats-catalog-storagev1placeplace_id (https://st.yandex-team.ru/EDACAT-1812)
* Каталог должен начать передавать в сервис слотов время доставки заказа до покупателя: EDACAT-1774

#### Интеграции
* Создают ручку получения слотов по place_origin_id без состава заказа
* Создают ручку получения слотов и длительности сборки по place_origin_id с составом заказа
* модицицируют ручку создания заказа:
 - Проверяют, что заказ сделан для Ленты
 - Идем в ручку eats-customer-slots %%POST /api/v1/place/get-picking-slots%% и получают слоты сборки
 - Получают лимит по заказу
 - Создают в Ленте заказ в слот
 - Прописывают в meta заказа информацию о слоте сборки (через интерфейс ОПГ)
* Создают ручку получения статуса заказа в Ленте
* Реализуют логику получения статуса заказа в Ленте, отмены заказа, создания новой ревизии, если состав заказа изменился в процессе сборки

#### eats-customer-slots
1. Заказываем сервису Postgres
2. Создаем в нем таблицы, хранящие слоты для каталога и слоты для чекаута
3. Пишем периодик, который обновляет слоты в таблице **partner_catalog_slots**, делая запросы в ручку интеграций.
4. Делаем кэш над этой таблицей
5. Меняем логику ручки слотов для каталога (получаем слоты сборки партнера)
6. Меняем логику ручки слотов для чекауте (начнаем принимать состав корзины, получаем слоты сборки партнера)
7. Делаем ручку, получения слота доставки по слоту сборки %%POST /api/v1/place/get-picking-slots%%:

#### ОПГ
* При получении заказа Ленты (смотрим по конфигу, что это именно Лента), сразу создаем заказ в Ленте
* Дописываем в meta заказа флаг wait_picking_data=true
* Релизаует интерфейс для записи информации о слоте сборки в meta заказа

#### Че2
* При получении заказа с флагом wait_picking_data идет в meta заказа и получает время окончания слота сборки а так же длительность сборки. По этим данным принимает решение о назначении курьера.

#### Каталог
* Принимает от коры place.origin_id и отдаем его из eats-catalog-storage
* Передает в сервис слотов время доставки заказа для каждого магазина

#### Итерсы
* Заводят новые причины отмен заказав

#### TeamA
* Отдают в каталог place.origin_id
* Возможно: заполняют поле calculate_slots_aware_info составом корзины


### Спеки новых и изменяемых ручек

#### Ручка интеграций `/api/v1/partner/get-picking-slots` получения слотов сборки от Ленты
```yaml
/api/v1/partner/get-picking-slots:
	post:
		summary: Получение слотов и длительности сборки по слотам доставки/флагу asap
		requestBody:
			required: true
			content:
				application/json:
			schema:
				type: object
				additionalProperties: false
				required:
				  - place_origin_id
				properties:
					place_origin_id:
						type: string
						desctiption: Идентификатор заведения в системе партнера
						example: 5500bc4b-c769-4309-8fda-5605c966f2a1
					items: 
						type: array
						items:
							type: object
							additionalProperties: false
							required:
				  			  - origin_id
				  			  - quantity
				  			properties:
				  				origin_id:
				  					type: string
				  					description: Идентификатор товара в системе партнера
				  					example: 5500bc4b-c769-4309-8fda-5605c966f2a1
				  				quantity:
				  					type: integer
				  					format: int64
									example: 1
									description: количество товара
		responses:
			200:
				description: Слоты сборки успешно найдены
				content:
					application/json:
				schema:
					type: object
					additionalProperties: false
					required:
					  - picking_slots
					properties:
						picking_slots:
							type: array
							description: Список слотов сборки у партнера
							required:
							  - slot_id
							  - from
							  - to
							  - duration
							items:
								type: object
								additionalProperties: false
								required:
									slot_id:
										type: string
										description: Идентификатор слота
									from:
										type: string
										format: date-time
										description: Начало слота доставки (UTC)
										example: "1937-01-01T12:00:27.870000+00:20"
									to:
										type: string
										format: date-time
										description: Начало слота доставки (UTC)
										example: "1937-01-01T12:00:27.870000+00:20"
									duration:
										type: integer
										desctiption: Продолжительность сборки в секундах
										x-taxi-cpp-type: std::chrono::seconds


			400:
				description: Ошибка в запросе
				content:
					application/json:
				schema:
					$ref: "#/components/schemas/ErrorResponse"
			401:
				description: Не пройдена авторизация
				content:
					application/json:
				schema:
					$ref: "#/components/schemas/ErrorResponse"
			404:
				description: Слоты сборки не найдены
				content:
					application/json:
				schema:
					$ref: "#/components/schemas/ErrorResponse"

components:
	schemas:
		ErrorResponse:
			type: object
				additionalProperties: false
				required:
				  - code
				  - message
				properties:
					code:
						type: string
						description: Код ошибки
						example: slots_not_found
					message:
						type: string
						description: Текст ошибки
						example: Значение не должно быть пустым.
```

#### Ручка eats-customer-slots `/api/v1/place/get-picking-slots` получения слотов сборки по слотам доставки
```yaml
/api/v1/place/get-picking-slots:
	post:
		summary: Получение слота сборки и длительности сборки у партнера по слоту доставки/флагу asap
		requestBody:
			required: true
				content:
					application/json:
				schema:
					type: object
					additionalProperties: false
					required:
					  - place_id
					  - user_id
					  - asap
					properties:
						place_id:
							type: string
							desctiption: Идентификатор заведения в Еде
						user_id: 
							type: string
							description: Идентификатор клиента в Еде (eater_id)
						delivery_slot_start:
							type: string
							format: date-time
							description: Начало слота сборки (UTC). Допустимо не передавать, если asap = true
							example: "1937-01-01T12:00:27.870000+00:20"
						delivery_slot_end:
							type: string
							format: date-time
							description: Конец слота сборки (UTC). Допустимо не передавать, если asap = true
							example: "1937-01-01T12:00:27.870000+00:20"
						delivery_duration:
							type: integer 
							x-taxi-cpp-type: std::chrono::seconds
							description: Оценочное время доставки заказа от магазина покупателю
						asap:
							type: boolean
							description: Флаг ASAP заказа
		responses:
			200:
				description: Слоты сборки успешно найдены
				content:
					application/json:
				schema:
					type: object
					additionalProperties: false
					required:
					  - place_id
					  - place_origin_id
					  - picking_duration
					  - picking_slots
					properties:
						place_id:
							type: string
							description: Идентификатор заведения в Еде
						place_origin_id:
							type: string
							description: Идентификатор заведения в системе партнера
						picking_slots:
							type: array
							items:
								type: object
								additionalProperties: false
								required:
								  - picking_slot_id
								  - picking_duration
								  - picking_slot_start
								  - picking_slot_end
								picking_slot_id:
									type: string
									description: Идентификатор слота сборки в системе партнера		
								picking_duration:
									type: integer
									x-taxi-cpp-type: std::chrono::seconds
									description: Оценочное время сборки у партнера
								picking_slot_start:
									type: string
									format: date-time
									description: Начало слота доставки (UTC)
									example: "1937-01-01T12:00:27.870000+00:20"
								picking_slot_end:
									type: string
									format: date-time
									description: Начало слота доставки (UTC)
									example: "1937-01-01T12:00:27.870000+00:20"

			400:
				description: Ошибка в запросе
				content:
					application/json:
				schema:
					$ref: "#/components/schemas/ErrorResponse"
			401:
				description: Не пройдена авторизация
				content:
					application/json:
				schema:
					$ref: "#/components/schemas/ErrorResponse"
			404:
				description: Слот сборки не найден
				content:
					application/json:
				schema:
					$ref: "#/components/schemas/ErrorResponse"
```
#### Изменение ручки eats-customer-slots `/api/v1/order/calculate-slots`
```yaml
cart_uid:
  description: уникальный код корзины
  type: string
items:
  type: array
  minItems: 1
  items:
      type: object
      additionalProperties: false
      required:
        - quantity
        - is_catch_weight
      properties:
          public_id:
              type: string
              description: Идентификатор товара из номенклатуры/eats-products. Должен быть обязательно, если не передан core_id.
          core_id:
              type: string
              description: Идентификатор товара в коре. Должен быть обязательно, если не передан public_id.
          quantity:
              type: integer
              description: Количество товара. Для штучных - штуки, для весовых - число квантов
          is_catch_weight:
              type: boolean
              description: Флаг указывающий весовой продукт, или нет
              example: false
```
#### Изменение ручки eats-customer-slots `/api/v1/places/calculate-delivery-time`
```yaml
places:
    description: |
        Массив заведений, для которых нужно вычислить стоимость доставки.
        Note: частично дублирует поле places_ids, которое оставлено для
        обратной совместимости.
    type: array
    minItems: 1
    items:
        type: object
        additionalProperties: false
        required:
          - place_id
          - estimated_delivery_duration
        properties:
            place_id:
                $ref: '#/components/schemas/PlaceId'
            estimated_delivery_duration:
                description: Ожидаемая длительность
                    доставки
                type: integer
                x-taxi-cpp-type: std::chrono::seconds

components:
    schemas:
        PlaceId:
            type: integer
            format: int64
```