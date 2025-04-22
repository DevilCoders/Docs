### Объекты на карте
 
`Map.StopPopup.Shown` — показ бабла «Расписание транспорта» рядом с пользователем (вместо TransportStopPopupDidShow)

Параметры:
* stop_id – id остановки
* CommonParams

`Map.StopPopup.Tapped` — тап пользователя по баблу «Расписание транспорта» (вместо TransportStopPopupDidTap)

Параметры:
* stop_id – id остановки
* CommonParams

`Map.Stop.Shown` — показ иконки остановки

Параметры:
* stop_id - id остановки
* CommonParams

`Map.Stop.Tapped` — тап пользователя по иконке остановки

Параметры:
* stop_id - id остановки
* CommonParams

`Map.TransportVehicle.Tapped` — тап по метке транспорта на карте (вместо TransportVehicleDidTap)

Параметры:
* route_id – id маршрута, по которому едет автобус
* vehicle_id – id кокретного автобуса/трамвая/тролейбуса
* CommonParams

### Карточка остановки

`StopCard.Shown` — показ карточки остановки (вместо TransportStopCardDidShow)

Параметры:
* open_reason - из-за чего появился элемент/Откуда открылась карточка
* map / route_card
* button_list - список кнопок
* select_route / back / close
* schedule - время прибытия транспорта. Словарь с номером/id маршрута и временем прибытия
* stop_id – id остановки
* CommonParams

`StopCard.Opened` — выдвижение вверх карточки остановки

Параметры:
* open_reason - из-за чего появился элемент/Откуда открылась карточка
* map / route_card
* button_list - список кнопок
* select_route / back / close
* schedule - время прибытия транспорта. (словарь, где ключ - id маршрута, значение - время до прибытия) - передаем только 5 ближайших маршрутов
* stop_id – id остановки
* CommonParams

`StopCard.Tapped` — тап на кнопку в карточке остановки

Параметры:
* open_reason - из-за чего появился элемент/Откуда открылась карточка
* map / route_card
* button_list - список кнопок на элементе
* select_route / back / close
* button_name - название кнопки, на которую нажали
* select_route / back / close
* route_id/taxi - номер маршрута (если тапнули на маршрут либо выбрали такси)
* stop_id – id остановки
* CommonParams

`StopCard.Scrolled` — скролл карточки остановки

Параметры:
* open_reason - из-за чего появился элемент/Откуда открылась карточка
* map / route_card
* direction_scroll - направление скролла
* up / down
* stop_id – id остановки
* CommonParams


`StopCard.Closed` — закрытие карточки остановки

Параметры:
* open_reason - из-за чего появился элемент/Откуда открылась карточка
* map / route_card
* close_reason - из-за чего скрылся элемент
* select_route / back / close / out_card (тап за пределами карточки) / roll_off (смахивание вниз)
* button_list - список кнопок
* select_route / back / close
* stop_id – id остановки
* CommonParams

`StopCard.Loaded` — загрузка карточки остановки с расписанием транспорта 

Параметры:
* code — код загрузки (400,500)
* stop_id - id остановки
* CommonParams

### Карточка маршрута

`TransportRouteCard.Shown` — показ карточки маршрута (вместо TransportRouteCardDidShow)

Параметры:
* route_id – id маршрута
* open_reason - из-за чего появился элемент/Откуда открылась карточка
* map / stop_card
* button_list - список кнопок
* back / close
* CommonParams

`TransportRouteCard.Opened` — выдвижение вверх карточки маршрута

Параметры:
* route_id – id маршрута
* open_reason - из-за чего появился элемент/Откуда открылась карточка
* map / stop_card
* button_list - список кнопок
* back / close
* CommonParams

`TransportRouteCard.Tapped` — тап на кнопку в карточке маршрута 

Параметры:
* route_id – id маршрута
* open_reason - из-за чего появился элемент/Откуда открылась карточка
* map / stop_card
* button_list - список кнопок на элементе
* back / close
* button_name - название кнопки, на которую нажали
* back / close
* stop_id - id остановки (если тапнули на остановку)
* CommonParams

`TransportRouteCard.Scrolled` — скролл карточки маршрута

Параметры:
* route_id – id маршрута
* open_reason - из-за чего появился элемент/Откуда открылась карточка
* map / stop_card
* direction_scroll - направление скролла
* up / down
* CommonParams

`TransportRouteCard.Closed` — закрытие карточки маршрута

Параметры:
* route_id – id маршрута
* open_reason - из-за чего появился элемент/Откуда открылась карточка
* map / stop_card
* close_reason - из-за чего скрылся элемент
* back / close / out_card (тап за пределами карточки) / roll_off (смахивание вниз)
* button_list - список кнопок
* back / close
* CommonParams

`TransportRouteCard.Loaded` — загрузка карточки маршрута со списком остановок 

Параметры:
* code — код загрузки (400,500)
* route_id - id маршрута
* CommonParams