Тул выбирает из БД b2bgeo_yacourier_prod маршруты, соответствующие условиям:
1. У курьера прописан телефон
1. Маршрут скоро начнется или уже начался и пора уведомить курьера

Для каждого такого маршрута:
1. Формируем диплинк вида `yandexnavi://build_route_on_map?... &yacourier=XXX&client=305&signature=NAVI_SIGNATURE`
    Подпись NAVI_SIGNATURE проверяется Навиком при открытии диплинка.
    В параметре yacourier закодированы в base64 параметры: 
    - `version`, всегда 1
    - `courier_id`, `route_id`
    - `tracking_begin`, `tracking_end` - интервал времени, за который сохраняем координаты курьера
    - `signature` - HMAC подпись для проверки, что диплинк создан нами
1. Укорачиваем диплинк с помощью ya.cc
1. Посылаем укороченный диплинк курьеру в СМС
