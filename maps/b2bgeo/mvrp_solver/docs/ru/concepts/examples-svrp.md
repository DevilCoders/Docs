
# Маршрутизация для одного курьера

Запрос к этому ресурсу строит маршрут для курьера с учетом дорожной ситуации и периодов доставки товара.

## Шаг 1. Отправьте запрос на создание маршрута


{% list tabs %}

- cURL

  **Запрос:**
  ``` bash
  curl -X POST "https://courier.yandex.ru/vrs/api/v1/add/svrp?apikey=<ваш API ключ>" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"depot\": {\"time_window\": \"07:00:00-23:59:59\",\"point\": {\"lat\": 55.751245,\"lon\": 37.618424}},\"locations\": [{\"time_window\": \"07:00:00-23:59:59\",\"point\": {\"lat\": 55.751245,\"lon\": 37.618424}}],\"vehicle\": {\"id\": 0}, \"options\":{\"time_zone\": 3}}"
  ```

  Запрос должен содержать полученный ключ. Если у вас нет ключа, оставьте заявку на подключение.

  **Ответ:**

  Ответ сервера содержит информацию о статусе обработки запроса.

  ``` JSON
  {
    "id": "4073f13e-ee1e-4f76-a990-725ace27f951",
    "status": {
      "queued": 1533895665.9222
    },
    "message": "Task queued"
  }
  ```
  Сохраните полученный id для использования на следующем шаге.

- Python

  Запрос на построение маршрута можно отправить с помощью библиотеки requests:

  ``` python
  #!/usr/bin/env python2.7
  import requests
  import time
  import datetime

  API_KEY = '<ваш API-ключ>'
  API_ROOT_ENDPOINT = 'https://courier.yandex.ru/vrs/api/v1'

  # Создайте тело запроса, включая склад, точки доставки, транспортное средство и настройки.
  payload = {
      'depot': {'id': 0, 'time_window': '07:00-23:59', 'point': {'lat': 55.733777, 'lon': 37.588118}},
      'locations': [
          {'id': 1, 'time_window': '09:00-20:00', 'point': {'lat': 55.684872, 'lon': 37.595965}},
          {'id': 2, 'time_window': '15:00-20:00', 'point': {'lat': 55.739796, 'lon': 37.689102}},
          {'id': 3, 'time_window': '12:00-15:00', 'point': {'lat': 55.809657, 'lon': 37.520314}},
          {'id': 4, 'time_window': '09:00-15:00', 'point': {'lat': 55.744764, 'lon': 37.558224}},
          {'id': 5, 'time_window': '15:00-20:00', 'point': {'lat': 55.788563, 'lon': 37.670101}},
      ],
      'vehicle': {'id': 0},
      'options':{'time_zone': 3}
  }

  # Отправьте запрос и получите ID поставленной задачи.
  response = requests.post(
      API_ROOT_ENDPOINT + '/add/svrp',
      params={'apikey': API_KEY}, json=payload)
  ```

- Node.js

  Запрос можно отправить с помощью модуля request:

  ``` JavaScript
  var request = require('request');

  // Создание тела запроса, включая склад, точки доставки, транспортное средство и настройки.
  var payload = {
      'depot': {'id': 0, 'time_window': '07:00-23:59', 'point': {'lat': 55.733777, 'lon': 37.588118}},
      'locations': [
          {'id': 1, 'time_window': '09:00-20:00', 'point': {'lat': 55.684872, 'lon': 37.595965}},
          {'id': 2, 'time_window': '15:00-20:00', 'point': {'lat': 55.739796, 'lon': 37.689102}},
          {'id': 3, 'time_window': '12:00-15:00', 'point': {'lat': 55.809657, 'lon': 37.520314}},
          {'id': 4, 'time_window': '09:00-15:00', 'point': {'lat': 55.744764, 'lon': 37.558224}},
          {'id': 5, 'time_window': '15:00-20:00', 'point': {'lat': 55.788563, 'lon': 37.670101}},
      ],
      'vehicle': {'id': 0},
      'options':{'time_zone': 3}
  };

  const API_KEY = '<ваш API-ключ>';
  const API_ROOT_ENDPOINT = 'https://courier.yandex.ru/vrs/api/v1'

  // Отправка запроса и получение ID поставленной задачи.
  function sendRequest(payload) {
      var url = API_ROOT_ENDPOINT + '/add/svrp?apikey=' + API_KEY;
      var options = {
          body: JSON.stringify(payload),
          headers: {'Content-Type': 'application/json'}
      }

      return new Promise(function(resolve, reject) {
          request.post(url, options, function(error, response, body) {
              if (error) { reject(error); }
              else {
                  var code = response.statusCode;
                  if (code == 201 || code == 202) {
                      resolve(JSON.parse(body).id);
                  } else {
                      reject(body);
                  }
              }
          })
      });
  }

  function handleError(error) {
      console.log('Error:', error);
  }

  // sendRequest(payload)
  //     .catch(handleError);
  ```

{% endlist %}

Информация о теле запроса доступна на странице сервиса.

## Шаг 2. Запросите результат обработки

Построенный маршрут можно получить с помощью GET-запроса к сервису.

{% list tabs %}

- cURL

  **Запрос:**
  ``` bash
  curl -X GET "https://courier.yandex.ru/vrs/api/v1/result/svrp/41231f83e-ee1e-4f76-a990-725dce27f951"
  ```

  **Ответ:**

  Если маршрут был построен, ответ будет содержать информацию о маршруте. В противном случае, ответ будет содержать информацию о статусе обработки запроса.

- Python

  ``` python
  # Дождитесь ответа.
  poll_stop_codes = {
      requests.codes.ok,
      requests.codes.gone,
      requests.codes.internal_server_error
  }

  # Опрос сервера о готовности результата оптимизации маршрута с использованием полученного ранее ID.
  if response.status_code == requests.codes.accepted:
      request_id = response.json()['id']
      poll_url = '{}/result/svrp/{}'.format(API_ROOT_ENDPOINT, request_id)

      response = requests.get(poll_url)
      while response.status_code not in poll_stop_codes:
          time.sleep(1)
          response = requests.get(poll_url)

      # Вывод информации в пользовательском формате.
      if response.status_code != 200:
          print 'Error {}: {}'.format(response.text, response.status_code)
      else:
          print 'Route optimization completed'
          print ''

          for route in response.json()['result']['routes']:
              print 'Vehicle {} route: {:.2f}km'.format(
                  route['vehicle_id'], route['metrics']['total_transit_distance_m'] / 1000)

              # Вывод маршрута в текстовом формате.
              for waypoint in route['route']:
                  print '  {type} {id} at {eta}, {distance:.2f}km driving '.format(
                      type=waypoint['node']['type'],
                      id=waypoint['node']['value']['id'],
                      eta=str(datetime.timedelta(seconds=waypoint['arrival_time_s'])),
                      distance=waypoint['transit_distance_m'] / 1000)

              # Вывод маршрута в формате ссылки на Яндекс.Карты.
              yamaps_url = 'https://yandex.ru/maps/?mode=routes&rtext='
              for waypoint in route['route']:
                  point = waypoint['node']['value']['point']
                  yamaps_url += '{}%2c{}~'.format(point['lat'], point['lon'])

              print ''
              print 'See route on Yandex.Maps:'
              print yamaps_url
  ```

-  Node.js

  ``` JavaScript
  // Опрос сервера о готовности результата оптимизации маршрута с использованием полученного ранее ID.
  function pollResponse(requestId) {
      function delay(t) {
          return new Promise(function(resolve) {
              setTimeout(resolve, t);
          });
      }

      function poller(resolve, reject) {
          function run() {
              let url = API_ROOT_ENDPOINT + '/result/svrp/' + requestId;

              request.get(url, function(error, response, body) {
                  if (error) { reject(error); }
                  else {
                      let result = JSON.parse(body);
                      let code = response.statusCode;
                      if (code != 200 && code != 410 && code != 500) {
                          delay(500).then(run);
                      } else {
                          if (code == 200) {
                              resolve(JSON.parse(body));
                          } else {
                              reject(body);
                          }
                      }
                  }
              });
          }
          run();
      }

      return new Promise(poller);
  }

  // Вывод информации в пользовательском формате.
  function printResponse(response) {
      console.log('Route optimization completed\n')

      for (route of response.result.routes) {
          let distance_km =
              (route.metrics.total_transit_distance_m / 1000).toFixed(2)

          console.log(`Vehicle ${route.vehicle_id} route: ${distance_km}km`);

          // Вывод маршрута в текстовом формате.
          for (waypoint of route.route) {
              let type = waypoint.node.type;
              let id = waypoint.node.value.id;
              let eta = new Date(waypoint.arrival_time_s * 1000).toISOString().substr(11, 8);
              let distance_km = (waypoint.transit_distance_m / 1000).toFixed(2);

              console.log(`  ${type} ${id} at ${eta}, ${distance_km}km driving `);
          }

          // Вывод маршрута в формате ссылки на Яндекс.Карты.
          let yamaps_url = 'https://yandex.ru/maps/?mode=routes&rtext='
          for (waypoint of route.route) {
              let point = waypoint.node.value.point;
              yamaps_url += `${point.lat}%2c${point.lon}~`;
          }

          console.log('\nSee route on Yandex.Maps:\n', yamaps_url)
      }
  }

  // Асинхронное выполнение функций.
  sendRequest(payload)
      .then(pollResponse)
      .then(printResponse)
      .catch(handleError);
  ```   

{% endlist %}


<p class="p"><a href="feedback.html" class="xref button">Написать в службу поддержки</a></p>
