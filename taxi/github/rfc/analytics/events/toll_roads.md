__**Объекты на карте**__

`Map.Route.Tapped` - тап по маршруту на карте

Параметры:
* mode - статус, в котором сейчас находится пользователь (main/summary/driving...)
* road_type – тип выбранной дороги (платная/бесплатная)
    * toll / free
* CommonParams

`Map.TollRouteBubble.Tapped` - тап по баблу "По платной дороге"

Параметры:
* mode - статус, в котором сейчас находится пользователь (main/summary/driving...)
* CommonParams

__**Карточка “Как поедете?”**__

`RoadSelectionCard.Shown` - показ карточки с выбором дороги (платной / бесплатной) при нажатии на Заказать

Параметры:
* button_list - список кнопок
    * done / close / high_demand_info
* road_type – тип выбранной дороги (платная/бесплатная)
    * toll / free
* CommonParams

`RoadSelectionCard.Tapped` - тап на кнопку к карточке с выбором дороги 

Параметры:
* button_list - список кнопок
    * done / close / high_demand_info
* button_name - название кнопки, на которую тапнули
    * done / close / high_demand_inf
* road_type – тип выбранной дороги (платная/бесплатная)
    * toll / free
* CommonParams

`RoadSelectionCard.Scrolled` - скролл карточки с выбором дороги 

Параметры:
* direction_scroll - направление скролла (up/down)
* road_type – тип выбранной дороги (платная/бесплатная)
* toll / free
* CommonParams

`RoadSelectionCard.Closed` - закрытие карточки с выбором дороги

Параметры:
* close_reason - из-за чего скрылся элемент (свернули / тапнули на карту / нажали на крестик / нажали “заказать”)
* roll_off / map_tapped / cancel_button / done / android_back_button
* button_list - список кнопок
* done / close / high_demand_info
* road_type – тип выбранной дороги (платная/бесплатная)
* toll / free
* CommonParams

__**Показ свитча**__
`СТАТУС_ПОЕЗДКИ.SwitchSelectionRoad` - переключение “По платной дороге" **(добавить событие во все возможные в данной функциональности статусы)**

Параметры:
* toll_road_switch: on/off – состояние свитча
* CommonParams

__**Алерт “На пути есть платная дорога”**__

`TollRoadAlert.Shown` - показ алерта “На пути есть платная дорога”

Параметры:
* road_type – тип выбранной дороги (платная/бесплатная)
* toll / free 
* button_list - список кнопок
* done
* CommonParams


`TollRoadAlert.Closed` - закрытие алерта “На пути есть платная дорога”

Параметры:
* close_reason - из-за чего скрылся элемент(свернули / тапнули на карту / нажали “заказать”)
* roll_off / map_tapped / done / android_back_button
* road_type – тип выбранной дороги (платная/бесплатная)
* toll / free 
* button_list - список кнопок
* done

`TollRoadAlert.Tapped` - тап на кнопку в алерте “На пути есть платная дорога”

Параметры:
* road_type – тип выбранной дороги (платная/бесплатная)
* toll / free 
* button_list - список кнопок
* done
* button_name - название кнопки, на которую тапнули
* done