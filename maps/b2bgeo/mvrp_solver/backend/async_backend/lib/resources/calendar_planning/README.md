## API
### POST /calendar_planning/tasks
Request body: solver request. <br>
Query params:
* `apikey` - apikey, required
* `lang` - locale


| Response codes |  |
| --- | --- |
| 202 | Success, task created |
| 400 | Client error, invalid query params |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 422 | Client error |
| 429 | Too many requests |
| 500 | Internal error |

#### Response
Success:
```
{
    "id": string,
    "status": string,
    "message": string
}
```
Error:
```
{
    "error": {
        "message": string,
        "incident_id": string
    }
}
```

### GET /calendar_planning/tasks/<task_id>/status
Query params:
* `apikey` - apikey, required
* `lang` - locale

| Response codes |  |
| --- | --- |
| 200 | Success |
| 400 | Client error, invalid query params |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 404 | Task not found |
| 500 | Internal error |

#### Response
Success:
```
{
    "id": string,
    "status": string,
    "message": string
}
```
Error:
```
{
    "error": {
        "message": string,
        "incident_id": string
    }
}
```


### GET /calendar_planning/tasks/<task_id>/result
Query params:
* `apikey` - apikey, required
* `lang` - locale

| Response codes |  |
| --- | --- |
| 200 | Success |
| 400 | Client error, invalid query params |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 404 | Task result not found |
| 500 | Internal error |

#### Response
Success: <br>
Solver response <br>
Error:
```
{
    "error": {
        "message": string,
        "incident_id": string
    }
}
```


### GET /calendar_planning/tasks/<task_id>/result/metadata
Query params:
* `apikey` - apikey, required
* `lang` - locale

| Response codes |  |
| --- | --- |
| 200 | Success |
| 400 | Client error, invalid query params |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 404 | Task result not found |
| 500 | Internal error |

#### Response
Success: <br>
```
{
    "dates": [
        {
            "date": string
        }
    ],
    "vehicles": [
        {
            "id": string
        }
    ],
    "dates_vehicles": [
        {
            "date": string,
            "vehicle_id": string
        }
    ]
}
```
<br>
Error:
```
{
    "error": {
        "message": string,
        "incident_id": string
    }
}
```

### GET /calendar_planning/tasks/<task_id>/result/filter
Query params:
* `apikey` - apikey, required
* `lang` - locale
* `date` - date, required
* `vehicle_id` - comma-separated list of vehicle ids

| Response codes |  |
| --- | --- |
| 200 | Success |
| 400 | Client error, invalid query params |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 404 | Task result or requested slice not found |
| 500 | Internal error |

#### Response
Success: <br>
Same as /result <br>
Error:
```
{
    "error": {
        "message": string,
        "incident_id": string
    }
}
```

### GET /calendar_planning/tasks/<task_id>/request
Query params: <br>
* `apikey` - apikey, required

| Response codes |  |
| --- | --- |
| 200 | Success |
| 400 | Client error, invalid query params |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 404 | Task not found |
| 500 | Internal error |

#### Response
Success: <br>
Unedited request <br>
Error: <br>
```
{
    "error": {
        "message": string,
        "incident_id": string
    }
}
```

### Task statuses
Possible status values:
* `queued`
* `running`
* `completed`
* `cancelled`
* `error`
* `internal_error`


## Example
```
curl -X POST "/calendar_planning/tasks?apikey=my_key" -d @task.json
202 Accepted
{"id": "task_id_1", "status": "queued", "message": "Task queued"}

curl "/calendar_planning/tasks/task_id_1/status?apikey=my_key"
200 OK
{"id": "task_id_1", "status": "running", "message": "Task is running and available for polling"}

curl "/calendar_planning/tasks/task_id_1/status?apikey=my_key"
200 OK
{"id": "task_id_1", "status": "completed", "message": "Task successfully completed"}

curl "/calendar_planning/tasks/task_id_1/result?apikey=my_key"
200 OK
{<solver result>}

curl "/calendar_planning/tasks/task_id_1/result/metadata?apikey=my_key"
200 OK
{
    "dates": [{"date": "2021-01-01"}, {"date": "2021-01-02"}],
    "vehciles": [{"id": "1"}],
    "vehicles_dates": [{"date": 2021-01-01, "vehcile_id": "1"}, {{"date": 2021-01-02, "vehcile_id": "1"}}]
}

curl "/calendar_planning/tasks/task_id_1/result/filter?date=2021-01-01&apikey=my_key"
200 OK
{<solver result>}
```
