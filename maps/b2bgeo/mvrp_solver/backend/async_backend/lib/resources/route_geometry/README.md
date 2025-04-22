## API
This API is designed to get the geometry of a specific route from a specific task to display it on the map.

Usage scenario:
1. Make a POST request to the `/vrs/api/v1/route/`.
2. If the response status is 200, the response payload contains the result.
3. Otherwise if the status is 202, the work is done asynchronously.
     1. Read `Retry-After` from headers to get needed poll period.
     2. Read `Location` from headers to get the location to poll.
     3. Poll the location with given interval while the status is not `303`.
     4. Get the result from location pointed by `Location` header.
4. It is possible to cancel route geometry task by POST request to the `/vrs/api/v1/route/<geometry_id>/cancel`.

Internal processing:
1. Download result of the task from s3.
2. Pull out route points, time intervals and characteristics of the vehicle from the task.
3. Request all pairs of route points from /debug_visualization handle of the matrix router.
If the matrix router cannot build part of the route between some pairs of points, this part of route will contain empty `geometry` field.

If we have N points in a route, the handle will return N-1 elements with geometries. Each element has `routing_mode` field which indicates which transportation mode (by car, by foot) is used.

### POST /vrs/api/v1/route/

Get a route geometry on the map for specific route in specific task. 

**Query params**
| parameter name | type | description |
|---|---|---|
| `apikey` | string | apikey, required |
| `lang` | string | locale |

**Query body**
| parameter name | type | description |
|---|---|---|
| `task_id` | uuid | Id of solved task, required |
| `run_number` | number | Number of run, required |
| `vehicle_id` | string | Vehicle ID, required |

**Example**
```
{
    "task_id" : "52eb837a-aa7b-49d2-bd40-b4e015560079",
    "run_number" : 1,
    "vehicle_id" : "Some ID",
}
```

<br>

**Response codes**

| response code  | comment | header |
| --- | --- | --- |
| 200 | OK, task finished (sync) | **Content-Type**:</br>text/json |
| 202 | Success, task created | **Location**: URL of status handle (`/vrs/api/v1/route/<geometry_id>/status`) |
| 400 | Client error, invalid query params |**Content-Type**:</br>text/json |
| 401 | Invalid apikey |**Content-Type**:</br>text/json |
| 402 | Banned apikey |**Content-Type**:</br>text/json |
| 403 | Forbidden |**Content-Type**:</br>text/json |
| 422 | Client error |**Content-Type**:</br>text/json |
| 429 | Too many requests |**Content-Type**:</br>text/json |
| 500 | Internal error |  |

**Response**<br>
OK, task finished (sync):
```
{
    "geometry_id" : string,
    "route" : [
        {
            "routing_mode" : "driving",
            "geometry" : 
            {
                "type": "LineString",
                "coordinates": [
                    [29.01, 40.01],
                    [29.02, 40.02],
                    [29.03, 40.03],
                    [29.04, 40.04]
                ]
            }
        },
        {
            "routing_mode" : "walking",
            "geometry" : 
            {
                "type": "LineString",
                "coordinates": [
                    [29.04, 40.04],
                    [29.05, 40.05],
                    [29.06, 40.06],
                    [29.07, 40.07]
                ]
            }
        },
        ...
    ]
}
```
Success, task created (async):
```
{
    "geometry_id" : string,
    "message": string
}
```
Error:
```
{
    "error": {
        "message": string,
        "incident_id" : string
    }
}
```

### GET /vrs/api/v1/route/<geometry_id>/status
**Query params**
| parameter name | type | description |
|---|---|---|
| `apikey` | string | apikey, required |
| `lang` | string | locale |

<br>

**Response codes**
| response code  | comment | header |
|---|---|---|
| 200 | Task running / queued, make request again in `Retry-After` seconds | **Retry-After**: seconds |
| 303 | Task is ready to pull from `Location` | **Location**: URL of result |
| 400 | Client error, invalid query params | **Content-Type**:</br>text/json |
| 401 | Invalid apikey | **Content-Type**:</br>text/json |
| 402 | Banned apikey | **Content-Type**:</br>text/json |
| 403 | Forbidden | **Content-Type**:</br>text/json |
| 404 | Geometry ID not found or task cancelled | **Content-Type**:</br>text/json |
| 410 | Server error, try to repeat original query to `/vrs/api/v1/route/` | **Content-Type**:</br>text/json |
| 500 | Internal error |  |

### POST /vrs/api/v1/route/<geometry_id>/cancel
**Query params**
| parameter name | type | description |
|---|---|---|
| `apikey` | string | apikey, required |
| `lang` | string | locale |

<br>

**Response codes**
| response code  | comment | header |
|---|---|---|
| 200 | Geometry task successfully cancelled | **Content-Type**:</br>text/json |
| 400 | Client error, invalid query params | **Content-Type**:</br>text/json |
| 401 | Invalid apikey | **Content-Type**:</br>text/json |
| 402 | Banned apikey | **Content-Type**:</br>text/json |
| 403 | Forbidden | **Content-Type**:</br>text/json |
| 404 | Geometry task not found or already completed/cancelled | **Content-Type**:</br>text/json |
| 500 | Internal error |  |

### GET /vrs/api/v1/route/<geometry_id>/result
**Query params**
| parameter name | type | description |
|---|---|---|
| `apikey` | string | apikey, required |
| `lang` | string | locale |

<br>

**Response codes**
| response code  | comment | header |
| --- | --- | --- |
| 200 | Success | **Content-Type**:</br>text/json |
| 400 | Client error, invalid query params |**Content-Type**:</br>text/json |
| 401 | Invalid apikey |**Content-Type**:</br>text/json |
| 402 | Banned apikey |**Content-Type**:</br>text/json |
| 403 | Forbidden |**Content-Type**:</br>text/json |
| 404 | Geometry ID not found or geometry task was cancelled or still running |**Content-Type**:</br>text/json |
| 410 | Server error, try to repeat original query to `/vrs/api/v1/route/` | **Content-Type**:</br>text/json |
| 500 | Internal error |  |

**Response**<br>
Success:
```
{
    "geometry_id" : string,
    "route" : [
        {
            "routing_mode" : "driving",
            "geometry" : 
            {
                "type": "LineString",
                "coordinates": [
                    [29.01, 40.01], //some geometry
                    [29.02, 40.01],
                    [29.03, 40.03],
                    [29.04, 40.04]
                ]
            }
        },
        {
            "routing_mode" : "walking",
            "geometry" : 
            {
                "type": "LineString",
                "coordinates": [
                    [29.04, 40.04], //some geometry
                    [29.05, 40.04],
                    [29.06, 40.04],
                    [29.07, 40.07]
                ]
            }
        },
        {
            "routing_mode" : "walking",
            "geometry" : 
            {} //case when matrix router cannot visualise route between points
        },
        ...
    ]
}
```
Error:

```
{
    "error": {
        "message": string,
        "incident_id" : string
    }
}
```
