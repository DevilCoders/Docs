### введение: связь между гипотезами и снимками
![alt text](https://jing.yandex-team.ru/files/naplavkov/graphviz-3.svg)

<details><summary>graphviz</summary><pre><code>

digraph db {
node [shape=record style=filled fontsize=8]

subgraph cluster_eye {
style=filled
color=azure2
label="EYE"

subgraph cluster_generate_hypothesis {
style=filled
color=azure3
href="https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/lib/generate_hypothesis/include/generator.h?rev=r9125713#L200"
label="generate_hypothesis"

hypothesis[label="{HYPOTHESIS}|{<hypothesis_id>hypothesis_id|}"]
hypothesis_object[label="{HYPOTHESIS_OBJECT}|{<object_id>object_id|<hypothesis_id>hypothesis_id}"]
}

subgraph cluster_object_manager {
style=filled
color=azure3
    href="https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/lib/object_manager/impl/object_manager.cpp?rev=r9122618#L353"
label="object_manager"

object[label="{OBJECT}|{<object_id>object_id|<primary_detection_id>primary_detection_id}"]
primary_detection_relation[label="{PRIMARY_DETECTION_RELATION}|{<primary_detection_id>primary_detection_id|<detection_id>detection_id}"]
}

subgraph cluster_sync_detection {
style=filled
color=azure3
href="https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/lib/sync_detection/impl/sync.cpp?rev=r9126270#L567"
label="sync_detection"

detection[label="{DETECTION}|{<detection_id>detection_id|<group_id> group_id}"]
detection_group[label="{DETECTION_GROUP}|{<group_id>group_id|<frame_id>frame_id}"]
}

subgraph cluster_import_mrc {
style=filled
color=azure3
href="https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/lib/import_mrc/impl/import.cpp?rev=r9126298#L279"
label="import_mrc"

feature_to_frame[label="{FEATURE_TO_FRAME}|{<frame_id>frame_id|<feature_id>feature_id}"]
}
}

subgraph cluster_signals {
style=filled
color=azure2
label="SIGNALS"

feature[label="{FEATURE}|{<feature_id>feature_id|}"]
}

hypothesis_object:hypothesis_id -> hypothesis:hypothesis_id
hypothesis_object:object_id  -> object:object_id
object:primary_detection_id -> detection:detection_id
detection:group_id -> detection_group:group_id
object:primary_detection_id -> primary_detection_relation:primary_detection_id
primary_detection_relation:detection_id -> detection:detection_id
detection_group:frame_id -> feature_to_frame:frame_id
feature_to_frame:feature_id -> feature:feature_id

}

</code></pre></details>

### в ЛК пользователя добавляем данные по сгенерированным на основе фотографий гипотезам

##### new table `rides.ride_hypothesis`
| Column        | Type   | Nullable |
| ------------- | ------ | -------- |
| ride_id       | bigint | not null |
| hypothesis_id | bigint | not null |

```
CREATE TABLE rides.ride_hypothesis (
    ride_id bigint NOT NULL REFERENCES rides.ride(ride_id),
    hypothesis_id bigint NOT NULL REFERENCES eye.hypothesis(hypothesis_id)
);
```

##### new field in [`RideContribution`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/contributions/mrc_ride.proto)
```
message Hypothesis {
    message Type {
        message AbsentTrafficLight {}
        message AbsentHouseNumber {}
        message WrongSpeedLimit {}
        message AbsentParking {}
        message WrongParkingFtType {}
        message TrafficSign {}
        message WrongDirection {}
        message ProhibitedPath {}
        message LaneHypothesis {}

        oneof type {
            AbsentTrafficLight absent_traffic_light = 1;
            AbsentHouseNumber absent_house_number = 2;
            WrongSpeedLimit wrong_speed_limit = 3;
            AbsentParking absent_parking = 4;
            WrongParkingFtType wrong_parking_ft_type = 5;
            TrafficSign traffic_sign = 6;
            WrongDirection wrong_direction = 7;
            ProhibitedPath prohibited_path = 8;
            LaneHypothesis lane_hypothesis = 9;
        }
    }

    required Type type = 1;
    optional string feedback_task_id = 2;
}

repeated Hypothesis hypotheses = 11;
```

##### измения в `ride_inspector`
- в функции [updateRides](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/ride_inspector/lib/ride.h?rev=r9078516#L16) обновляем таблицу `rides.ride_hypothesis`
- реагируем на появление гипотез, используя [eye.hypothesis_feedback.txn_id](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/libs/db/include/eye/hypothesis_gateway.h?rev=r9122618#L47)

##### измения в `ugc_uploader`
- данные таблицы `rides.ride_hypothesis` сериализует в `RideContribution`
