# Создание черновика нового заказа

Запрос позволяет создать черновик заказа.

{% note warning %}

Отправка данного запроса не начинает обработку заказа.

{% endnote %}


Чтобы начать обработку, необходимо выполнить запрос [Обработка заказа](processing.md), передав идентификатор заказа, полученный на этапе создания черновика. Данная схема позволяет избежать возможного дублирования заказов при сетевых ошибках.

{% note warning %}

Черновики заказов не нужно удалять вручную, они удаляются автоматически через 10-20 минут после создания.

{% endnote %}


## Синтаксис запроса

```
POST https://business.taxi.yandex.ru/api/1.0/client/{идентификатор клиента}/order/
```

Заголовки запроса:

#### Authorization
OAuth-токен. Процесс получения токена описан в разделе [Начало работы](quickstart.md).

Данные о заказе передаются в теле запроса в формате JSON. Структура полей приведена в разделе [Пример запроса](#req-ex).

#|
||**Поле** | **Описание** | **Формат** ||
||`comment` | Комментарий клиента. | Строка ||
||`fullname` | Имя и фамилия клиента. | Строка ||
||`phone` | Телефонный номер клиента. | Строка ||
||`due` | Время посадки. Указывается, только если заказ создается на будущее к определенному времени.  Формат значений: `YYYY-MM-DDThh:mm:ss(±hhmm)`. | Строка ||
||`source` | Блок с информацией о точке начала поездки. Содержит следующие поля:<br/><br/>- `country`;<br/>- `fullname`;<br/>- `geopoint`;<br/>- `locality`;<br/>- `porchnumber`;<br/>- `premisenumber`;<br/>- `thoroughfare`. | Объект ||
||`source.country` | Страна. | Строка ||
||`source.fullname` | Полный адрес. | Строка ||
||`source.geopoint` | Координаты точки назначения. Формат параметра:``` [долгота,широта] ``` | Массив ||
||`source.locality` | Населенный пункт. | Строка ||
||`source.porchnumber` | Номер подъезда. | Строка ||
||`source.premisenumber` | Номер дома и корпуса. | Строка ||
||`source.thoroughfare` | Название улицы или микрорайона (для адресов с нумерацией по микрорайону). | Строка ||
||`source.extra_data` | Дополнительная информация о доставке посылок от двери до двери. Объект может быть вложен в объект `source` (содержит информацию об отправителе) или в объект `destination` (содержит информацию о получателе). <br/>

{% note warning %}

Объект доступен только для тарифов `express` и `courier` (задается в поле [class](#class-desc)) c указанным требованием `door_to_door` (задается в поле [requirements](#requirements-desc)).<br/><br/>

{% endnote %}

Содержит следующие поля:<br/>
```json
"contact_phone": "+79031111111", "floor": "1", "apartment": "1", "comment": "my comment" \
```
- `contact_phone` — телефон получателя/отправителя. Формат: строка.
- `floor` — этаж отправителя/получателя. Формат: строка.
- `apartment` — квартира отправителя/получателя. Формат: строка.
- `comment` — комментарий к доставке. Формат: строка. | Объект ||
||`interim_destinations` | Блок с информацией о промежуточных точках поездки. Список полей каждого объекта идентичен блоку [source](#source-desc). | Массив объектов ||
||`destination` | Блок с информацией о точке завершения поездки. Список полей идентичен блоку [source](#source-desc). | Объект ||
||`offer` | [Оффер поездки](route-stats.md#offer-param). | Строка ||
||`class` | Тариф поездки. Обязательное поле. | Строка ||
||`requirements` | Блок с требованиями к заказу.

{% cut "Подробнее" %}

Список требований к заказу может варьироваться в зависимости от города. Чтобы узнать поддерживаемые требования, отправьте пустой объект `{}` в теле POST-запроса `https://business.taxi.yandex.ru/client-api/3.0/cities`. В ответе будет содержаться список городов. Названия городов указаны в поле `city`, а поддерживаемые требования и их коды будут перечислены в массиве `"supported_requirements"`.

{% endcut %}

 | Объект ||
||`nosmoking` | Признак некурящего водителя. | Логическое ||
||`cost_center` | Название [центра затрат клиента](cost-center-create-old.md). Поле игнорируется при наличии в запросе поля `cost_center_values`. | Строка ||
||`cost_center_values` | Новые поля [центров затрат](cost-center-settings-list.md). | Массив ||
||`cost_center_values.[N].id` | id поля [центров затрат](cost-center-settings-list.md). | Строка ||
||`cost_center_values.[N].title` | Название поля [центров затрат](cost-center-settings-list.md). | Строка ||
||`cost_center_values.[N].value` | Значение поля [центров затрат](cost-center-settings-list.md) для данного заказа. | Строка ||
|#

Список требований к заказу может варьироваться в зависимости от города. Чтобы узнать поддерживаемые требования, отправьте пустой объект `{}` в теле POST-запроса `https://business.taxi.yandex.ru/client-api/3.0/cities`. В ответе будет содержаться список городов. Названия городов указаны в поле `city`, а поддерживаемые требования и их коды будут перечислены в массиве `"supported_requirements"`.

Пример запроса:

```
curl -d"{}" https://business.taxi.yandex.ru/client-api/3.0/cities
...
Authorization: <OAuth-токен>
```

## Описание полей ответа

В ответе могут содержаться следующие поля:

Поле | Описание | Формат
----- | ----- | -----
`_id` | Идентификационный номер заказа. | Строка


## Пример запроса {#req-ex}

{% list tabs %}

- Создание заказа на вызов такси

	```json
	POST https://business.taxi.yandex.ru/api/1.0/client/a2...d09/order/


	{
		"comment": "some comment",
		"fullname": "Имя Фамилия",
		"phone": "+71112223344",
		"due": "2013-04-01T14:00:00+0400",
		"source": {
			 "country": "Россия",
			 "fullname": "Россия, Москва, Новосущевская, 1",
			 "geopoint": [
				 33.6,
				 55.1
			 ],
			 "locality": "Москва",
			 "porchnumber": "1",
			 "premisenumber": "1",
			 "thoroughfare": "Новосущевская"
		},
		"interim_destinations": [{
			"country": "Россия",
			"fullname": "Россия, Москва, Троицкая, 15с1",
			"geopoint": [
				37.6,
				55.7
			],
			"locality": "Москва",
			"porchnumber": "",
			"premisenumber": "15с1",
			"thoroughfare": "Троицкая"
		}],
		"destination": {
			"country": "Россия",
			"fullname": "Россия, Москва, 8 Марта, 4",
			"geopoint": [
				33.1,
				52.1
			],
			"locality": "Москва",
			"porchnumber": "",
			"premisenumber": "4",
			"thoroughfare": "8 Марта"
		},
		"class": "econom",
		"requirements": {
			"nosmoking": true
		},
		"cost_center": "some cost center",
		"cost_center_values": [
			{
				"id": "cost_center",
				"title": "Цель поездки",
				"value": "производственная необходимость"
			},
			{
				"id": "0123456789abcdef0123456789abcde1",
				"title": "Цель поездки",
				"value": "особая цель"
			}
		]
	}
	```

- Создание заказа на доставку от двери до двери

	```json
	POST https://business.taxi.yandex.ru/api/1.0/client/a2...d09/order/


	{
	  "comment": "",
	  "source": {
		  "country": "Россия",
		  "fullname": "Россия, Москва, улица Льва Толстого, 16",
		  "short_text": "улица Льва Толстого, 16",
		  "short_text_from": "улица Льва Толстого, 16",
		  "short_text_to": "улица Льва Толстого, 16",
		  "geopoint": [
			  37.587093,
			  55.733969
		  ],
		  "locality": "Москва",
		  "premisenumber": "16",
		  "thoroughfare": "улица Льва Толстого",
		  "type": "address",
		  "object_type": "другое",
		  "extra_data": {
			  "contact_phone": "+79031111111",
			  "floor": "1",
			  "apartment": "1",
			  "comment": "my comment"
		  }
	  },
	  "class": "express",
	  "requirements": {"door_to_door": true},
	  "phone": "+79811234567",
	  "destination": {
		  "country": "Россия",
		  "fullname": "Россия, Москва, Тверской бульвар, 1",
		  "short_text": "Тверской бульвар, 1",
		  "short_text_from": "Тверской бульвар, 1",
		  "short_text_to": "Тверской бульвар, 1",
		  "geopoint": [
			  37.597765,
			  55.757992 
		  ],
		  "locality": "Москва",
		  "premisenumber": "27с1",
		  "thoroughfare": "Тверской бульвар",
		  "type": "address",
		  "object_type": "другое",
		  "extra_data": {
			  "contact_phone": "+79032222222",
			  "floor": "2",
			  "apartment": "123",
			  "comment": "33"
		  },
	  "cost_center": "some cost center"
	  }
	}
	```

{% endlist %}

## Пример ответа

Пример ответа на данный запрос выглядит следующим образом:

```no-highlight
{
        "_id": "3caa3587675b49deb62e3286b753b05e"
}
```

## Возможные коды ответа

{% include [cost-center-create-possible-answers-code](../_includes/concepts/cost-center-create/id-cost-center-create/possible-answers-code.md) %}


- `200` — запрос выполнен успешно.
- `401` — был передан неверный [OAuth-токен](quickstart.md).
- `404 UNKNOWN_CITY` — невозможно создать черновик заказа в данном городе.
- `406 EMPTY_CORP_PAYMENTMETHODS` - отсутствуют активные способы корп.оплаты для указанного пользователя.
- `406 GENERAL` - ошибка при проверке возможности сделать заказ, точная причина указана в теле ответа в поле `message`.
- `406 GENERAL` с причиной `Cannot create order` - временная техническая ошибка.
- `406 INACTIVE_USER` — невозможно создать черновик заказа для неактивного пользователя.
- `406 TARIFF_IS_UNAVAILABLE` — невозможно создать черновик заказа с указанным тарифом.

