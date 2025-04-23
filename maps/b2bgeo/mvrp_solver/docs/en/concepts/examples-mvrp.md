# Routing for multiple couriers

A request to this resource distributes orders across couriers while taking vehicle capacity into account. After orders are distributed, the service builds the optimal delivery route.

## Step 1. Send a request to build a route

{% list tabs %}

- cURL

  **Request:**

  ```bash
  curl -X POST "https://courier.yandex.ru/vrs/api/v1/add/mvrp?apikey=<yout API key>" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"depot\": {\"point\": {\"lat\": 55.751245,\"lon\": 37.618424},\"time_window\": \"07:00:00-23:59:59\"},\"locations\": [{\"point\": {\"lat\": 55.751245,\"lon\": 37.618424},\"time_window\": \"07:00:00-23:59:59\"}],\"vehicles\": [{\"capacity\": {\"volume\": {\"depth_m\": 10,\"height_m\": 10,\"width_m\": 10}},\"id\": 1,\"shifts\": [{\"id\": \"42\",\"time_window\": \"07:00:00-23:59:59\"}],\"visited_locations\": [{\"id\": 12}]}], \"options\":{\"time_zone\": 3, \"quality\": \"normal\"}}"
  ```

  The request must contain the API key you received earlier. If you don't have a key, apply for it.

  **Response:**

  The server response contains the request processing status.

  ```JSON
  {  
     "id":"f74a0efc-f9a1-4643-b834-9769fabaee7b",
     "status":{  
        "queued":1534160155.189995
     },
     "message":"Task queued"
  }
  ```

  Save the received ID. You'll need it at the next step.

- Python

  You can send a request to build a route using the requests library:

  ```python
  #!/usr/bin/env python2.7
  import requests
  import time
  import datetime
  
  API_KEY = '<your API key>'
  API_ROOT_ENDPOINT = 'https://courier.yandex.ru/vrs/api/v1'
  
  # Create the request body, including the depot, delivery destinations, vehicle, and settings.
  payload = {
      "depot": {"point": {"lat": 55.751245,"lon": 37.618424},"time_window": "07:00:00-23:59:59"},
      "locations": [
          {'id': 1, 'time_window': '09:00-20:00', 'point': {'lat': 55.684872, 'lon': 37.595965}},
          {'id': 2, 'time_window': '15:00-20:00', 'point': {'lat': 55.739796, 'lon': 37.689102}},
          {'id': 3, 'time_window': '12:00-15:00', 'point': {'lat': 55.809657, 'lon': 37.520314}},
          {'id': 4, 'time_window': '09:00-15:00', 'point': {'lat': 55.744764, 'lon': 37.558224}},
          {'id': 5, 'time_window': '15:00-20:00', 'point': {'lat': 55.788563, 'lon': 37.670101}}
      ],
      "vehicles": [
          {"capacity": {"volume": {"depth_m": 10,"height_m": 10,"width_m": 10}},"id": 1,"shifts": [{"id": "42","time_window": "07:00:00-23:59:59"}],"visited_locations": [{"id": 1}]}
      ],
      "options":{"time_zone": 3, "quality": "normal"}
  
  }
  
  # Send your request and get the ID of the task assigned.
  response = requests.post(
      API_ROOT_ENDPOINT + '/add/mvrp',
      params={'apikey': API_KEY}, json=payload)
  ```

- Node.js

  You can send a request using the request module:

  ```JavaScript
  var request = require('request');
  
  // Creating the request body, including the depot, delivery destinations, vehicle, and settings.
  var payload = {
      "depot": {"point": {"lat": 55.751245,"lon": 37.618424},"time_window": "07:00:00-23:59:59"},
      "locations": [
          {'id': 1, 'time_window': '09:00-20:00', 'point': {'lat': 55.684872, 'lon': 37.595965}},
          {'id': 2, 'time_window': '15:00-20:00', 'point': {'lat': 55.739796, 'lon': 37.689102}},
          {'id': 3, 'time_window': '12:00-15:00', 'point': {'lat': 55.809657, 'lon': 37.520314}},
          {'id': 4, 'time_window': '09:00-15:00', 'point': {'lat': 55.744764, 'lon': 37.558224}},
          {'id': 5, 'time_window': '15:00-20:00', 'point': {'lat': 55.788563, 'lon': 37.670101}}
      ],
      "vehicles": [
          {"capacity": {"volume": {"depth_m": 10,"height_m": 10,"width_m": 10}},"id": 1,"shifts": [{"id": "42","time_window": "07:00:00-23:59:59"}],"visited_locations": [{"id": 1}]}
      ],
      "options":{"time_zone": 3, "quality": "normal"}
  
  };
  
  const API_KEY = '<your API key>';
  const API_ROOT_ENDPOINT = 'https://courier.yandex.ru/vrs/api/v1'
  
  // Sending the request and getting the ID of the task assigned.
  function sendRequest(payload) {
      var url = API_ROOT_ENDPOINT + '/add/mvrp?apikey=' + API_KEY;
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

Information about the request body is available on the service page.

## Step 2. Request the processing result

You can obtain the resulting route using a GET request to the service.

{% list tabs %}

- cURL

  **Request:**

  ```bash
  curl -X GET "https://courier.yandex.ru/vrs/api/v1/result/mvrp/ID_задачи"
  ```

  **Response:**

  If the route is built, route details are included in the response. Otherwise, the response contains the request status.

- Python

  ```python
  
  # Wait for a response.
  poll_stop_codes = {
      requests.codes.ok,
      requests.codes.gone,
      requests.codes.internal_server_error
  }
  
  # Using the previously received ID to poll the server for whether the route optimization result is available.
  if response.status_code == requests.codes.accepted:
      request_id = response.json()['id']
      poll_url = '{}/result/mvrp/{}'.format(API_ROOT_ENDPOINT, request_id)
  
      response = requests.get(poll_url)
      while response.status_code not in poll_stop_codes:
          time.sleep(1)
          response = requests.get(poll_url)
  
      # Displaying information in a custom format.
      if response.status_code != 200:
          print 'Error {}: {}'.format(response.text, response.status_code)
      else:
          print 'Route optimization completed'
          print ''
  
          for route in response.json()['result']['routes']:
              print 'Vehicle {} route: {:.2f}km'.format(
                  route['vehicle_id'], route['metrics']['total_transit_distance_m'] / 1000)
  
              # Displaying the route in text format.
              for waypoint in route['route']:
                  print '  {type} {id} at {eta}, {distance:.2f}km driving '.format(
                      type=waypoint['node']['type'],
                      id=waypoint['node']['value']['id'],
                      eta=str(datetime.timedelta(seconds=waypoint['arrival_time_s'])),
                      distance=waypoint['transit_distance_m'] / 1000)
  
              # Displaying the route as a link to Yandex.Maps.
              yamaps_url = 'https://yandex.ru/maps/?mode=routes&rtext='
              for waypoint in route['route']:
                  point = waypoint['node']['value']['point']
                  yamaps_url += '{}%2c{}~'.format(point['lat'], point['lon'])
  
              print ''
              print 'See route on Yandex.Maps:'
              print yamaps_url
  ```

- Node.js

  ```JavaScript
  // Using the previously received ID to poll the server for whether the route optimization result is available.
  function pollResponse(requestId) {
      function delay(t) {
          return new Promise(function(resolve) {
              setTimeout(resolve, t);
          });
      }
  
      function poller(resolve, reject) {
          function run() {
              let url = API_ROOT_ENDPOINT + '/result/mvrp/' + requestId;
  
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
  
  // Displaying information in a custom format.
  function printResponse(response) {
      console.log('Route optimization completed\n')
  
      for (route of response.result.routes) {
          let distance_km =
              (route.metrics.total_transit_distance_m / 1000).toFixed(2)
  
          console.log(`Vehicle ${route.vehicle_id} route: ${distance_km}km`);
  
          // Displaying the route in text format.
          for (waypoint of route.route) {
              let type = waypoint.node.type;
              let id = waypoint.node.value.id;
              let eta = new Date(waypoint.arrival_time_s * 1000).toISOString().substr(11, 8);
              let distance_km = (waypoint.transit_distance_m / 1000).toFixed(2);
  
              console.log(`  ${type} ${id} at ${eta}, ${distance_km}km driving `);
          }
  
          // Displaying the route as a link to Yandex.Maps.
          let yamaps_url = 'https://yandex.ru/maps/?mode=routes&rtext='
          for (waypoint of route.route) {
              let point = waypoint.node.value.point;
              yamaps_url += `${point.lat}%2c${point.lon}~`;
          }
  
          console.log('\nSee route on Yandex.Maps:\n', yamaps_url)
      }
  }
  
  // Asynchronous function execution.
  sendRequest(payload)
      .then(pollResponse)
      .then(printResponse)
      .catch(handleError);
  ```

{% endlist %}

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>

