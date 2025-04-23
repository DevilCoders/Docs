## MRC UGC Account service

This document describes the API of the MRC UGC Service which is a complement for the [Maps UGC Account service](/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/Api.md).

MRC UGC Service API implements the following use-cases:
- show detailed info about a user's ride
- show/hide authorship for a whole ride
- delete starting and ending part of a ride
- delete a ride


### Request requirements
Each request must be performed with TVM `ServiceTicket` and `UserTicket`.


### Headers
* `X-Ya-Service-Ticket`
* `X-Ya-User-Ticket`
* `X-Ya-Sync-Token` synchronization token, response to every modification request
  contains this token. The Token must be included in the following requests in order to guarantee the response data freshness.
* Accept: `application/x-protobuf`(default) or `text/x-protobuf`


### Response codes
| HTTP code | Response | Explanation |
|---|---|---
| 200 Ok | | |
| 400 Bad Request |  | Request parameters malformed |
| 401 Unauthorized |  | No valid user or service ticket |
| 403 Forbidden |  | User does not have access to this object |
| 404 Not Found |  | Handler or object not found |
| 429 Too Many Requests  |  | Rps quota exceeded |
| 500 Internal Server Error |  | Contact developers |


### Contribution objects

MRC UGC service provides the following contribution presentations:
- MRC_RIDE_CONTRIBUTION


#### MRC_RIDE_CONTRIBUTION
Contains brief information about a ride.

```(c++)
mrc_ride {
  id: "1"
  started_at {
    value: 1605873286
    tz_offset: 0
    text: "2020-11-20T11:54:46"
  }
  finished_at {
    value: 1605874286
    tz_offset: 0
    text: "2020-11-20T12:11:26"
  }
  duration {
    value: 3600.0
    text: "1 hour"
  }
  distance {
    value: 1000.0
    text: "1 km"
  }
  photos_count: 3
  album_image {
    url_template: "https://mrc-browser.maps.yandex.ru/v1/rides/my/album_image?ride_id=1&size="
    size {
      size: "48x27"
      width: 48
      height: 27
    }
  }
  ride_status {
    pending {
    }
  }
  client_ride_id: "b0c2d8c8-6fc6-45d0-9e8e-45e37bd29636"
  published_photos_count: 1
  hypotheses {
    type {
      absent_traffic_light {
      }
    }
    feedback_task_id: "42"
  }
  hypotheses {
    type {
      absent_house_number {
      }
    }
    feedback_task_id: "100500"
  }
}
```

### Endpoints

#### **GET /v1/rides/my/get**

This method is used to get detailed info about a user's ride.

| **Method** | GET |
|------------|-----|
| **Parameters** |
| ride_id | ride id |
| **Response body** |
| yandex.maps.proto.mrcugc.ride.MyRide |

Example response:
```(c++)
id: "1"
started_at {
  value: 1605873286
  tz_offset: 0
  text: "2020-11-20T11:54:46"
}
finished_at {
  value: 1605874286
  tz_offset: 0
  text: "2020-11-20T12:11:26"
}
duration {
  value: 3600.0
  text: "1 hour"
}
distance {
  value: 1000.0
  text: "1 km"
}
photos_count: 3
track {
  lons {
    first: 37247873
    deltas: 141449
    deltas: 219726
  }
  lats {
    first: 55563219
    deltas: 94833
    deltas: 127892
  }
}
bbox {
  lower_corner {
    lon: 37.247873
    lat: 55.563219
  }
  upper_corner {
    lon: 37.609048
    lat: 55.785944
  }
}
show_authorship: true
track_preview {
  preview {
    items {
      position {
        segment_index: 0
        segment_position: 0.0
      }
      photo_id: "1"
    }
    items {
      position {
        segment_index: 0
        segment_position: 0.9
      }
    }
    items {
      position {
        segment_index: 1
        segment_position: 0.2
      }
      photo_id: "2"
    }
    items {
      position {
        segment_index: 1
        segment_position: 0.5
      }
      photo_id: "3"
    }
  }
  chunk_list {
    chunks {
      subpolyline {
        begin {
          segment_index: 0
          segment_position: 0.0
        }
        end {
          segment_index: 0
          segment_position: 1.0
        }
      }
      chunk_descriptor {
        payload: "data for request 1"
      }
      photos_count: 1
    }
    chunks {
      subpolyline {
        begin {
          segment_index: 0
          segment_position: 1.0
        }
        end {
          segment_index: 1
          segment_position: 1.0
        }
      }
      chunk_descriptor {
        payload: "data for request 2"
      }
      photos_count: 2
    }
  }
}
client_ride_id: "b0c2d8c8-6fc6-45d0-9e8e-45e37bd29636"
published_photos_count: 1
hypotheses {
  type {
    absent_traffic_light {
    }
  }
  feedback_task_id: "42"
}
hypotheses {
  type {
    absent_house_number {
    }
  }
  feedback_task_id: "100500"
}
```


#### **POST /v1/rides/my/chunk**

Annotates part of user's track with photo ids.

| **Method** | POST |
|------------|-----|
| **Parameters** |
| **Request body** |
| yandex.maps.proto.mrcugc.ride.TrackPreview.ChunkDescriptor |
| **Response body** |
| yandex.maps.proto.mrcugc.ride.TrackChunk |

Response body
```(c++)
photos {
  items {
    position {
      segment_index: 0
      segment_position: 0.0
    }
    photo_id: "1"
  }
  items {
    position {
      segment_index: 0
      segment_position: 0.9
    }
  }
}
```

#### **GET /v1/rides/my/photo**

Gets a photo from the ride by id.

| **Method** | GET |
|------------|-----|
| **Parameters** |
| id | photo's identifier |
| **Response body** |
| yandex.maps.proto.mrcugc.ride.MyPhoto |


Example response:

```(c++)
id: "1"
taken_at {
  value: 1605873286
  tz_offset: 0
  text: "2020-11-20T11:54:46"
}
geo_photo {
  image {
    url_template: "https://core-nmaps-mrc-browser.maps.yandex.ru/v1/rides/my/photo_image?photo_id=1&size_name="
    size {
      size: "48x27"
      width: 48
      height: 27
    }
    size {
      size: "1600x1080"
      width: 1600
      height: 1080
    }
  }
  shooting_point {
    point {
      point {
        lon: 37.247873
        lat: 55.563219
      }
    }
    direction {
      azimuth: 90.0
      tilt: 0.0
    }
  }
}
next_photo {
  photo_id: "2"
  shooting_point {
    point {
      point {
        lon: 37.247873
        lat: 55.563219
      }
    }
  }
}
```

#### **PUT /v1/rides/my/update**

Updates ride attributes:
- show/hide authorship for
- delete part(s) of the ride:
  * if both `delete_photos_after_photo_id` and `delete_photos_before_photo_id` are present
    in the request and `delete_photos_after_photo_id <= delete_photos_before_photo_id`
    then the part of the ride defined by the interval
    `[delete_photos_after_photo_id, delete_photos_before_photo_id]` is deleted.
  * otherwise starting/ending parts of the ride defied by intervals
    `[rideStart, delete_photos_before_photo_id)` and
    `(delete_photos_after_photo_id, rideEnd]` are deleted.

| **Method** | PUT |
|------------|-----|
| **Parameters** |
| ride_id | ride id |
| **Request body** |
| yandex.maps.proto.mrcugc.ride.UpdateRideRequest |
| **Response body** |
| yandex.maps.proto.mrcugc.ride.MyRide |

Example request:
```(c++)
show_authorship: true
delete_photos_after_photo_id: "2"
```


#### **DELETE /v1/rides/my/delete**

Deletes whole ride. The ride also disappears from the user's contributions list in the UGC account.

| **Method** | DELETE |
|------------|-----|
| **Parameters** |
| ride_id | ride id |


#### **GET /v1/rides/my/stat**

This method is used to get aggregated statistics about user's rides.

| **Method** | GET |
|------------|-----|
| **Parameters** |
| **Response body** |
| yandex.maps.proto.mrcugc.ride.MyStat |

Example response:
```(c++)
rides_count: 12
total_duration {
  value: 36000.0
  text: "10 hours"
}
total_distance {
  value: 15000.0
  text: "15 km"
}
total_photos_count: 1730
total_published_photos_count: 678

```

#### **DELETE /v1/walk_objects/my/delete**

Deletes walk object contribution in UGC account and mark photos of this object unpublished.

| **Method** | DELETE |
|------------|-----|
| **Parameters** |
| id | walk object id |
