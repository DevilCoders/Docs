# Zero speed banner (a.k.a. standing segments)

## General description
Zero Speed Banner (ZSB) is part of automobile routing service that provides functionality to show ads to users. This document elaborates on implementation details of the current solution that has been deployed for 100% users in both Russia and Turkey. The principal scheme looks like this:
1. During routing process a catboost model is used, it marks edges of the route that should be considered as candidates for ZSB.
2. The constructed route with the above mentioned markup is transferred to the client.
3. During the driving process the client monitors the user's movement speed. If it drops almost to 0 km/h then a stop is detected. If the stop occurs on a marked edge, we attempt to start showing ads. Movement is detected as soon as the user sets into motion. In this case the ad impression process is terminated.
4. There is a cooldown between two successive ad impressions. Currently it is set to 1 minute.

In Navi user interface ZSB looks like this:

![ZSB example](https://wiki.yandex-team.ru/geo/quality/documentation/zsb/.files/image-9.png "ZSB example")

Technical details follow.

##
| Key | Value |
|---|---|
| Contacts | Dmitry Kornev [(tswr@)](https://staff.yandex-team.ru/tswr) |
| Sources | https://a.yandex-team.ru/arc/trunk/arcadia//maps/routing/zero_speed_banner/ <br/> https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsZeroSpeedBannerPipeline <br/> https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/libs/directions/navigation/guides/standing_guide |
| Sandbox scheduler | https://sandbox.yandex-team.ru/scheduler/18602/view |
| Ecstatic dataset | [yandex-maps-zero-speed-banner-data](http://ecstatic.maps.yandex.net/pkg/yandex-maps-zero-speed-banner-data/versions) |


## ML model
We use a catboost model to detect places where users might stand for a long enough period of time. This model considers features of the current edge and three further edges on the route. We apply this model consecutively to each edge on the route to select candidates.

### Features

The following edge features are beeing used in [production](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/navigator_stopwatch/standing_detector.cpp?rev=6661721#L71)
* [road graph features](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/navigator_stopwatch/standing_detector.cpp?rev=6661721#L23):
  * presence of a traffic light at the end of the edge,
  * edge length,
* [jams statistical features](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/navigator_stopwatch/include/speed_banner_types.h?rev=6661721#L13) for the last two weeks extracted from [travel times](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/travel_times&):
  * average speed,
  * number of signals,
  * 10, 15, 20, 25 speed percentiles,
  * ratios of 55 percentile to 45, 60 to 40, 70 to 30, 75 to 25.

Full features list available for training can be found [here](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/zero_speed_banner/train_model/columns.json?rev=5829812#L1).

### Model training
Scripts for model training and their descriptions are located in [/maps/routing/zero_speed_banner](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/zero_speed_banner?rev=5829812). In order to obtain ground-truth and to assemble the training dataset we use mapkit-sims. To gather them consult innocent@. Run `build_model_pool` to build the training dataset and `train_model` to train the model.

### Keeping jams statics up to date
Jams statistics are prone to seasonal changes, that's why we regularly update them for each edge of the road graph. This task is carried out in sandbox.

## ZSB implementation in router
### Source code
The main code is in [/maps/routing/navigator_stopwatch/stopwatch.cpp](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/navigator_stopwatch/stopwatch.cpp#L786). List of uri handles that provide the edge markup can be found in [request_handlers.cpp](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router/yacare/bin/request_handlers.cpp?rev=6578316#L1). Currently it is:
* `GET /v2/route`,
* `GET /v2/predicted_route`,
* `POST /v2/alternatives`,
* `POST /v2/nearby_alternatives`,
* `POST /v2/reroute`.

### How to view the markup
In order to view the markup one can use `/debug_me` mode in router.

Go to [/maps/routing/router](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router#instances). Follow the Instances `stable` link to nanny. Locate `Current: ACTIVE` block. Press `Instances`. Copy the url and add `/debug_me`. You should get something like http://maps-core-driving-router-stable-1.sas.yp-c.yandex.net/debug_me . Select start and finish points by clicking on the map. In the right-hand side `Settings` area select `Standings segments` from the drop-down list `No markers`. Markup is depicted on the route with red color.

![ZSB markup](https://jing.yandex-team.ru/files/mlevkov/Screenshot%202020-04-15%20at%2016.20.06.png "ZSB markup")

## ZSB implementation in MapKit
MapRit code resides in [directions/guidance/location_guide/standing_detector.cpp](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/libs/directions/guidance/location_guide/standing_detector.cpp#L198).

## Experiments
Historically there were two implementations of ZSB:
* server side + mapkit client side,
* client side only solution in Navi.

As of today (15.04.2020) only the first one is used. But we still await MapKit / Navi with the latest changes to be released. Until then we [run](http://ab.yandex-team.ru/config/52) two 100% A/B experiments for version <= 4.49:
* Russia: [EXPERIMENTS-37165](https://st.yandex-team.ru/EXPERIMENTS-37165), testid [[183304]](https://ab.yandex-team.ru/testid/183304),
* Turkey: [EXPERIMENTS-38715](https://st.yandex-team.ru/EXPERIMENTS-38715), testid [[191543]](https://ab.yandex-team.ru/testid/191543),

and one experiments for version >= 4.50:
* Russia + Turkey: testid [[233595]](https://ab.yandex-team.ru/testid/233595).

## How to prepare `events` table:

1. [install pkg-root](https://wiki.yandex-team.ru/jandekskarty/development/fordevelopers/mobile/infra/newdev/)
2. clone mapsmobi repo
3. patch with [this](https://paste.yandex-team.ru/842307/) (diff was actual for repo version on 17.10.19). fix build errors
4. call `gradle install_deps@linux && gradle -PINSTALL pkg@linux` for `libs/mapkit` and `libs/mapkit/directions`
5. set [here](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/tools/mapkit_location_quality/__main__.py?rev=5105550#L50) `max_failed_jobs_count` to `10000`
6. `~/arcadia/maps/mobile/server/tools/mapkit_location_quality/mapkit_location_quality -i //home/navigator-user-report/daily-reports/2019-08-08 -o $OUTPUT_YT_TABLE -p $PATH_TO_PKG_ROOT -b $PATH_TO_MAPSMOBI/tools/location-quality/build/ya/linux/app/location-quality -t LogEvents -v $GRAPH_VERSION`
7. when yt job almost done gracefully stop it. mapkit reports sometimes contain invalid data, so some jobs will never succeed
