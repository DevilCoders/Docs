# Dashboards API

## Получение списка рецептов {#get-recipes}

GET-запрос на `v2/services_dashboards/catalog/<dashboard_id>/recipes/`

```json
GET /v2/services_dashboards/catalog/demo/recipes/ HTTP/1.1
Accept: application/json
Authorization: OAuth XXX
Host: nanny.yandex-team.ru

HTTP/1.1 200 OK
Content-Type: application/json

{
    "result": [
        {
            "content": {
                ...
            },
            "dashboard_id": "demo",
            "id": "test_1"
        }
    ]
}
```

## Получение содержимого рецепта {#get-recipe-content}

GET-запрос на `/v2/services_dashboards/catalog/<dashboard_id>/recipes/<recipe_id>/`

```json
GET /v2/services_dashboards/catalog/demo/recipes/test_1/ HTTP/1.1
Accept: application/json
Authorization: OAuth XXX
Host: nanny.yandex-team.ru

HTTP/1.1 200 OK
Content-Type: application/json

{
    "content": {
        "dependencies": [
            {
                "child": {
                    "id": "d6428f32-0497-4166-a733-9e1408770aeb"
                },
                "id": "66a95915-39ea-4d03-bb78-11c2f8bd3627",
                "parent": {
                    "id": "start"
                }
            },
            {
                "child": {
                    "id": "85756169-0809-4942-9b8e-72f451afcd3b"
                },
                "id": "2d8df2d4-fa50-4526-a66f-37f5792b3746",
                "parent": {
                    "id": "d6428f32-0497-4166-a733-9e1408770aeb"
                }
            }
        ],
        "name": "test_1",
        "start": {
            "graph_position": {
                "height": 30,
                "width": 30,
                "x": 2235,
                "y": 2485
            }
        },
        "tasks": [
            {
                "data": {
                    "name": "set_snapshot_target_state",
                    "params": {
                        "activate_recipe_id": "default",
                        "prepare_recipe_id": "default",
                        "service_id": "demo_service_1",
                        "target_state": "ACTIVE",
                        "wait_for_success": true
                    },
                    "vars": {}
                },
                "flags": {
                    "banned": false,
                    "manually_confirmed": false,
                    "skipped": false
                },
                "graph_position": {
                    "height": 120,
                    "width": 200,
                    "x": 2315,
                    "y": 2440
                },
                "id": "d6428f32-0497-4166-a733-9e1408770aeb"
            },
            {
                "data": {
                    "name": "set_snapshot_target_state",
                    "params": {
                        "activate_recipe_id": "default",
                        "prepare_recipe_id": "default",
                        "service_id": "demo_service_2",
                        "target_state": "ACTIVE",
                        "wait_for_success": true
                    },
                    "vars": {}
                },
                "flags": {
                    "banned": false,
                    "manually_confirmed": false,
                    "skipped": false
                },
                "graph_position": {
                    "height": 120,
                    "width": 200,
                    "x": 2565,
                    "y": 2440
                },
                "id": "85756169-0809-4942-9b8e-72f451afcd3b"
            }
        ]
    },
    "dashboard_id": "demo",
    "id": "test_1"
}
```

## Создание рецепта {#create-recipe}

POST на `/v2/services_dashboards/catalog/<dashboard_id>/recipes/`

Пример создания пустого графа:

```json
POST /v2/services_dashboards/catalog/demo/recipes/ HTTP/1.1
Accept: application/json
Authorization: OAuth XXX
Host: nanny.yandex-team.ru

{
    "id":  "test_2",
    "content": {
        "name": "test_2",
        "desc": "test_2",
        "tasks": [],
        "dependencies": [],
        "start":{
            "graph_position": {"x": 2485,"y": 2485,"width": 30,"height": 30}
        }
     }
}

HTTP/1.1 201 OK
Content-Type: application/json

{
  "dashboard_id": "demo",
  "id":"test_2",
  "content":{
    "start": {"graph_position": {"y": 2485,"x": 2485,"height": 30,"width": 30}},
    "tasks": [],
    "name": "test_2",
    "dependencies": [],
    "desc": "test_2"
  }
}
```

## Запуск выкатки дашборда {#deploy}

```python
import requests
import json

URL = 'https://nanny.yandex-team.ru'
OAUTH_TOKEN = 'XXX'
headers = {
    'Content-Type': 'application/json',
    'Authorization': 'OAuth {}'.format(OAUTH_TOKEN),
}

# получить содержимое дашборда
DASHBOARD_ID = 'demo'
resp = requests.get(URL + '/v2/services_dashboards/catalog/' + DASHBOARD_ID, headers=headers)
data = resp.json()
# print json.dumps(data, indent=4)

# получить содержимое рецепта
RECIPE_ID = 'test_1'
resp = requests.get(URL + '/v2/services_dashboards/catalog/' + DASHBOARD_ID + '/recipes/' + RECIPE_ID, headers=headers)
data = resp.json()
# print json.dumps(data, indent=4)

deploy_request = {
    'id': data['id'],
    'content': data['content'],
}

# присвоить всем set_snapshot_target_state-таскам идентификаторы снапшотов для выкатки
for task in deploy_request['content']['tasks']:
    task_data = task['data']
    if task_data['name'] != 'set_snapshot_target_state':
        continue
    service_id = task_data['params']['service_id']
    # получить идентификатор последнего снапшота
    current_runtime_attrs_id = requests.get(URL + '/v2/services/' + service_id, headers=headers).json()['runtime_attrs']['_id']
    task_data['vars']['snapshot_id'] = current_runtime_attrs_id

# отправить запрос на деплой
resp = requests.post(URL + '/v2/services_dashboards/catalog/' + DASHBOARD_ID + '/deployments/', headers=headers, json=deploy_request)
```

##  Отмена запущенного рецепта {#reject}

POST на `/v1/alemate/task_groups/search-XXXXXXXXXX/status/`
контент: `{"status":"REJECTED"}`.

