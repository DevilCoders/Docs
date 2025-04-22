# Получение заказов драйва в супераппе

### Задача
Отображать в супераппе такси заказы пользователя в драйве.

### Описание решения
1. Для ручки получения активных заказов драйва создаём прокси 
на стороне бэкенда такси (далее упоминается как `drive/tracking`);
2. Получаем из `drive/tracking` информацию о наличии и статусе заказа пользователся и 
отдаём её в `launch` и `/orders/state` (проставляем у заказов service: "drive") 
3. Клиенты осуществляют поллинг актуального статуса и другой другой информации о заказе
через вызов `drive/tracking` через PA.

---

### Создание прокси для ручки драйва

Создание прокси для внешней ручки даёт нам: 
  * Унификацию API;
  * Фильтрация лишних полей в ответе драйва;
  * Мониторинг ошибок из коробки;
  * Возможность управления нагрузкой посредством кэширования;

Документация ручки Драйва: https://wiki.yandex-team.ru/YANDEX.drive/carsharing/razrabotka/externalsession/

#### API

path: `/4.0/mlutp/v1/drive/v1/orders/tracking`

request:

body:
```json
{
    "location": [37.504381, 55.730800],
    "orders":[
        {
            "orderid":"order1",
            "tag": "encoded_part_tag"
        }
    ]
}
```
headers:
```
X-AppMetrica-DeviceId
X-AppMetrica-UUID
X-Ya-Service-Ticket
X-Ya-User-Ticket
```

response: 
```json
{
    "orders": [
        {
            "segment": {
                "session": {
                    "specials": {
                        "current_offer": {
                            "destination_name": "Работа", // куда едем
                            "device_id": "C59C****DD84",
                            "type": "fix_point",          // тип – фикс
                            "finish_area_border": [       // зеленая зона фикса, LONLAT
                                [37.6383386, 55.74207971],
                                [37.6412998, 55.74309649],
                                [37.6455484, 55.73631743],
                                [37.6419864, 55.73435612],
                                [37.6383386, 55.74207971]
                            ],
                            "finish": "37.64037323 55.73671341", // точка, куда едем LON LAT
                            "offer_id": "6c09bcdc-1e6376a0-55f972-97a1949f",
                            "pack_price": 13100,          // стоимость фикса
                            "name": "Фикс"                // название тарифа
                        }
                    },
                    // текущая стадия поездки
                    // old_state_reservation – бронь
                    // old_state_acceptance – приемка
                    // old_state_riding – поездка
                    // old_state_parking – ожидание
                    "current_performing": "old_state_reservation" 
                },
                "session_acceptance_start": 1590934408,   // timestamp начала приемки
                "session_acceptance_finish": 1590934408,  // timestamp конца приемки
                "meta": {
                    "start": 1590934407,   // timestmap начала поездки
                    "finished": true,      // флаг завершенности сессии
                    "finish": 1590934427,  // timestamp конца поездки
                    "session_id": "30410a49-4aaf876b-3804cb29-c79142a"
                }
            },
            "views": [ // массив моделей
                {
                    "image_map_url_2x": "https://carsharing.s3.yandex.net/drive/car-models/kia_rio_xline/map-2x.png?r=3",
                    "name": "KIA Rio X-Line",
                    "code": "kia_rio_xline",
                    "manufacturer": "KIA",
                    "image_angle_url": "https://carsharing.s3.yandex.net/drive/car-models/kia_rio_xline/kia-rio-xline-31-05.png",
                    "image_map_url_3x": "https://carsharing.s3.yandex.net/drive/car-models/kia_rio_xline/map-3x.png?r=3",
                    "registry_manufacturer": "",
                    "short_name": "X-Line",
                    "image_large_url": "https://carsharing.s3.yandex.net/drive/car-models/kia_rio_xline/kia-rio-xline-side-2-mow_large.png",
                    "visual": {
                        "background": {
                            "gradient": {
                                "bottom_color": "#F5F5F5",
                                "top_color": "#F5F5F5"
                            }
                        },
                        "title": {
                            "color": "#1A1E1F"
                        }
                    },
                    "image_pin_url_3x": "https://carsharing.s3.yandex.net/drive/pins/feb2020/2white-map-pin__feb2020-2@3x.png",
                    "image_small_url": "https://carsharing.s3.yandex.net/drive/car-models/kia_rio_xline/kia-rio-xline-side-2-mow_small.png",
                    "rank": -10,
                    "fuel_type": "95",
                    "fuel_cap_side": "left",
                    "image_pin_url_2x": "https://carsharing.s3.yandex.net/drive/pins/feb2020/2white-map-pin__feb2020-2@2x.png",
                    "registry_model": "",
                    "fuel_icon_url": "https://carsharing.s3.yandex.net/fuel_finger.png"
                }
            ],
            "car": {
                "number": "б811вг530", // ГРЗ машины
                "model_id": "mercedes_e200_w",
                "id": "16289305-48db-4351-9c5e-d74eee3e7227", // индекс модели машины в массиве views
                "location": { 
                    "lat": 55.7075882,
                    "lon": 37.68834305
                }
            }
        }
    ]
}
```

---

### Изменения на клиентах
На клиентах необходимо добавить новый part_type `drive_orders_tracking` для поллинга из ручки драйва
и, соответственно, описать поля request/response (см. секцию [API](#api))

---

##  Реализация

### Этап 1

1. [TAXIBACKEND-29617](https://st.yandex-team.ru/TAXIBACKEND-29617)
   - оценка: 3d
   - описание: Создание прокси ручки `drive/tracking` в superapp-misc для внутренней ручки драйва;
     Тэги и кэширование не поддерживаются (пока), ручка возвращает полную информацию о запрошенных заказах.

2. [TAXIBACKEND-29618](https://st.yandex-team.ru/TAXIBACKEND-29618)
   - оценка: 1d
   - описание: Проксирование из ПА во внутреннюю ручку `drive/tracking`

3. [TAXIBACKEND-29619](https://st.yandex-team.ru/TAXIBACKEND-29619)
   - оценка: 2d
   - описание: Реализация в api-proxy запроса в `drive/tracking` из `orders/state` для получения заказов из `launch`;

4. Создание на клиенте нового part_type


### Этап 2

Тэги, кэширование
