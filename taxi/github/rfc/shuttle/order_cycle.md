# Поллинг букингов shuttle клиентами

## /4.0/shuttle-control/v1/booking/list

Ручка для получения активных заказов при старте приложения. Такси заказы получаются через launch, чтобы его не усложнять, делаем отдельную ручку.
Статусы заказа:
- waiting (?) - статус, когда мы забронировали маршрутку, однако ее еще нет на линии (пребукинг).
- driving - статус, когда маршрутка на линии и едет к остановке посадки.
- transporting - статус, в который переходит заказ при "подборе" пассажира.
- finished - статус, в который переходит заказ при высадке пассажира.
- cancelled - статус, в который переходит заказ в случае отмены заказа по инициативе пользователя или бэкенда.

Возможные переходы:
- waiting: driving, cancelled (маршрутка не вышла на линию в назначенный срок; отмена клиентом)
- driving: transporting, cancelled (отмена клиентом ИЛИ водителем (неясно как))
- transporting: finished, cancelled (кажется вероятно, если например во время поездки произошла проблема с автомобилем, и заказ отменен через админку)
- finished: терминальный стейт
- cancelled: терминальный стейт

```
GET /4.0/shuttle-control/v1/booking/list

Response:
{
	"bookings": [
		{
			"booking_id": "UUID1",
			"status": "driving"
		}
	]
}
```

## /4.0/shuttle-control/v1/booking/information

Ручка для поллинга статуса букинга, по сути аналог totw. Отдает всю необходимую информацию для отображения плашки.
По 1 циклу поллинга на каждый активный букинг.
Частота поллинга управляется хедером X-Polling-Delay, выставляемым бекендом.

Для получения маршрута движения Шаттла (аналог taxiroute) предлагается пока использовать masstransit/lineinfo.
В перспективе заменить на условный shuttleroute.

Для того, чтобы можно было отобразить данные, где шаттл/пеший маршрут до точки B/куда идти не дожидаясь ответа lineinfo, в ответе есть координаты объектов - остановок, шаттла, точек A и B.

Ручка может отвечать:
- 200 OK - бронирование существует.
- 404 NotFound - бронирования не существует (невалидный booking_id).

После ответа 200 OK от ручки /4.0/shuttle-control/v1/shuttle/book, клиент начинает опрашивать ручку информации.
Если получает cancelled, то отображает причину и перестает поллить.
Если получает finished, то есть варианты:
- если мы делаем оценку поездки, то надо чтобы пришел флаг о возможности оставить фидбек (в available_actions?)
- если не делаем, то клиент просто отображает текст с бека "вы приехали", и заканчивает поллинг.

```
GET /4.0/shuttle-control/v1/booking/information?booking_id=UUID1

Response:
{
	"booking_id": "UUID1",
	"status": "driving",
	"available_actions": ["cancel"], // enum: {cancel}
	"route": {
		"route_id": "route_id1",
		"pickup_stop": {
			"id": "pickup_stop_id",
			"position": [3.0, 4.0]
		},
		"dropoff_stop": {
			"id": "dropoff_stop_id",
			"position": [4.0, 4.0]
		}
	},
	"source_point": {
	  "position": [1.0, 2.0],
		"full_text": "Россия, Москва, Садовническая улица, 82с1",
		"short_text": "Садовническая улица, 82с1",
		"uri": "ymapsbm1://org?oid=1009383031"
	},
	"destination_point": {
		"position": [5.0, 5.0],
		"full_text": "Россия, Москва, Садовническая улица, 82с2",
		"short_text": "Садовническая улица, 82с2",
		"uri": "ymapsbm1://org?oid=1009383123"
	}
	"shuttle": {
		"id": "shuttle_id1",
		"position": [3.0, 4.0],
		"azimuth": 98
		"icon": "car",
		"car_number": "XXX"
	},
	"ui": {
		"panel": {
			"title": "1 мин и приедет",
			"subtitle": "Пройдите к остановке",
			"icon_tag": "shuttle_icon"
		},
		"estimated_waiting": { // as in routestats
			"seconds": 60,
			"message": "1 min"
		}
	}
}

If booking was cancelled (by backend):
{
	"booking_id": "UUID1",
	"status": "cancelled",
	"ui": {
		"panel": {
			"title": "Сожалеем, заказ был отменен",
			"subtitle": "Шаттл перестал выходить на связь",
			"icon_tag": "shuttle_icon"
		}
	}
}
```
