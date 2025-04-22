Часть ответа                                        |Сервис                | Ручка |
----------------------------------------------------|----------------------|-------|
  `"currency_rules": {}`|  order-core  |  order-info  |
  `"dont_call": false`|
  `"dont_sms": true`|
  `"payment": { "type": "cash" }`|
  `"source": [ ]` // Просто request.route.0|
  `"request": {}`|
  `"status": "driving"`|
  `"tariff": {}`|
  `"version": "DAAAAAAA"`|
||
||
  `"cost_message": "От 100 $SIGN$$CURRENCY$"`|order_info|cost|
  `"cost_message": 100`|
  `"cost_message_details": {}`|
  `"final_cost": 100`|
  `"coupon": {}` // просто забирает из прока, нет смысла отделять |
  `"discount": {}` // почти то же самое, что coupon, странно|
  `"paid_supply_discount": {} `// скидка, если нашелся водитель поближе, только на основании прока | 
||
||
  `"allowed_changes": [ ]`||changes|
  `"payment_changes": [ ]`|
  `"pending_changes": [ ]`|
  `"user_ready": false`| // такое изменение есть в allowed_changes, поэтому пусть будет здесь
||
||
  `"route_sharing_url": "https://taxi.yandex.ru/route/c35dd2632adebdd917428f7036a0882a"`||route_sharing|
||
||
  `"extra_contact_phone": "" `||extra_contact_phone|
||
||
  `"higher_class_dialog": {}`||granted_promotions|
  `"granted_promotions": [ ]`|
||
||
  `"cost_message": "От 100"` // Здесь остается отмена. Забираем косты отсюда при отмене, иначе - из ручки cost|order_canceller|cancel|
  `"cost_message": 100`|
  `"cost_message_details": {}`|
  `"final_cost": 100`|
||
||
  `"cancel_disabled": false`||cancel_info|
  `"cancel_rules": { }`|
  `"free_cancel_for_reason": false`|
  `"cancelled_by": "" `
||
||
  `"driver": { `|performer_info|driver_info|
   `"name": "", `// Основные данные о водителе(имя, автомобиль итд)|
   `}`|
||
||
  `"button_modifiers": {} `||deaf_driver|
  `"force_destination": {} `|
||
||
  `"park": {}`| |park_info|
  `"partner": {}`|
||
||
  `"driver": {"car": {}}  `|order_route_info | driver_pos|
  `"driver": {"overdue": false}  `|
||
||
  `"exact_pickup_point": [ ]`| | route_info|
  `"routeinfo": {`|
   `"distance_left": 484`|
   `"time_left": 76`|
   `"max_time_left": 76`|
   `"positions": []`|
  `}`|
||
||
  `"freecars": {} ` // ||candidates_cars|
  `"busycars": {} `|
||
||
   `"driver": {"forwarding": {}} `|order_phones|driver_phone|
   `"driver": {"phone": {}, } `||
||
||
  `"loyal": false`|user-api|user_phones/get|
||
||
  `driverclientchat_enabled": true`|chat|check_enabled|
||
||
  `"status_info": {}` |preorder|status_info|
  `"max_waiting_time": ""`|
  `"departure_time": ""`|
||
||
  `"status_info": {}` |hourly_rental|status_info|
  `"max_waiting_time": ""`|
  `"departure_time": ""`|
||
||
  `"reorder": {} `|reorder|suggest_reorder|
  `"surge": {} `|
||
||
  `"autoreorder": {} `||autoreorder|
||
||
  `"reorder": {} `|reorder|order_info|
  `"autoreorder": {} `|
  `"surge": {} `|  
||
||
  `"order_name": {} `|multiorder|order_info|
  `"can_make_more_orders": "not_modified"`|
  `"no_more_orders_reason": ""`|
||
||
  `"code_dispatch": {}`|code_dispatch|order_info|
||
||
  `"brandings": [ { "stories": [] } ]`| taxi-stories|4.0/stories|
||
||
  `"tips": { }`|tips|order_tips|
||
||
  `"tips_suggestions": {}`||tips_suggestions|
||
||
  `"feedback": {}`| feedback|2.0/retrieve|
||
||
  `"supported_feedback_choices": {`| feedback_info|low_rating_reason|
   `"low_rating_reason": []`|
  `}`|
||
||
  `"supported_feedback_choices": {`||feedback_badges|
   `"feedback_badges": []`|
   `"feedback_rating_mapping": []`|
  `}`|
||
||
  `"typed_experiments": { }`|exp3-matcher|v1/experiments|
||
||
  `"status_info_title": { }` // pool|garbage||
  `"cancel_reason_description": {}` // pool|
  `"photo_url": "", ` // По словам Леши Холодкова, это легаси. Есть некоторая прослойка клиентов, которая получает урл фото из totw, новые уже получают из order_performer. Пока полгода до полного переезда пройдет, клиентов в этой прослойке станет достаточно мало|
