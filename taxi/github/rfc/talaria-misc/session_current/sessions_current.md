## Session current
GET [`/v1/user`](v1_user_response.json) - получить данные о пользователе включая текущую поездку  
POST [`/v1/boardRides`](v1_boardrides.json) - создание поездки  
GET [`/v1/boards/:boardId`](v1_board_boardId.json) - данные по конкретному самокату  
POST [`/v1/boardRides/reservation`](v1_board_rides_reservation.json) - бук самоката  
POST [`/v1/boardRides/:rideId`](v1_board_rides_ride_id.json) - Данные по текущей поездке  
DELETE [`/v1/boardRides/reservation/:rideId`](delete_v1_board_rides_revervation_rideid.json) - удаление бронирования  

В данный момен есть информация о коллег из Wind что максимальная нагрузка которую готовы держать ручки 200RPS.

Для получения текущей активной поездки необходимо получить данные из ручки `/v1/user -> user.currentRideId` , затем получить данные о текущей поездки из ручки `/v1/boardRides/:rideId`, для данных из блока `telematics` и `model_id` необходимо получить данные из ручки `/v1/boards/:boardId`  

Так как для сборка ответа необходимо опрашивать 3 виндовые ручки, возможно есть смысл над тем чтобы распилить ручку на 2 более легкие (требует обсуждения)

```javascript
{
    "extra_sessions_available": true, //  wind always false?
    "user": {
    "flags": {
      "enable_insurance": true //  always false for wind?
    },
    "cars_meta": {
        "models": {
            "ninebot": {
                "name": "Ninebot" //  board.boardType, may be null
            }
        }
    },
    "server_time": 1638535402,
    "sessions": [
      {
        "segment": {
          "car_number": "133", // board..boardNo
          "session": {
            "specials": {
              "current_offer": {
                "constructor_id": "scooters_minutes", // for wind always scooters_minutes?
                "offer_id": "eb2bc9c0-7ae4bb9f-4bf41c70-d0d641e0", // ride.rideId from /v1/boardRides
                "type": "standart_offer", // wind always standar_offer?
                "prices": {
                  "parking": 100, 
                  "riding": 600, // ride.price
                  "free_reservation": 300 // ride.priceModel.freeReservationSeconds
                }
              },
              "free_time": 106, // ride.priceModel.freeReservationSeconds
              "total_price": 0, // ride.totalCost
              "total_price_hr": "0 ₽"
              "total_duration": 0, // ride.costSummary.rideDuration
              "durations_by_tags": {
                "old_state_parking": 193 // time in seconds for this type of state /reservation/parking/riding
              }
            },
            "current_performing": "old_state_reservation" // текущий стэйт поездки, возможны: old_state_reservation, old_state_parking, old_state_riding (расказано далее)
          },
          "meta": {
            "start": 1638438888,
            "session_id": "f71188c8-ecac053f-2f98f1b-189426ad", // for wind we can use rideId
            "finished": false
          }
        }
      }
    ],
    "cars": [
      {
        "number": "133", // board.boardno
        "model_id": "ninebot", // ride.boardType
        "id": "1a2d121f-90ee-a2ee-3d7b-db21e6085675", // ride.boardId
        "location": {
          "lat": 59.955143,  // ride.startLatitude  
          "lon": 30.403412,  // ride.startLongitude
          "course": 0 // ?
        },
        "telematics": {
          "fuel_level": 10, // board.vol
          "fuel_distance": 105.1, // board.estimatedrange
          "remaining_time": 100 // (board.estimatedrange / 12) * 3600
        }
      }
    ]
  }
```

## Api tags
Для того чтобы на сервере понимать какой конкретный бекенд хочет полить клиент в данный момент, необходимо в полинговую ручку передавать `api_tag`, ниже представленна схема того откуда клиентам брать `api_tag`
![image](https://jing.yandex-team.ru/files/d-zaytsev/api_tag_schema.jpg)
