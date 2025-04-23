### Иерархия signals.track_point

#### Отличия signals.assignment_track_point

| Column        | Type   | Nullable |
| ------------- | ------ | -------- |
| assignment_id | bigint | not null |

```
Indexes:
    "assignment_track_point_assignment_id_index" btree (assignment_id)
Foreign-key constraints:
    "assignment_track_point_assignment_id_fkey" FOREIGN KEY (assignment_id) REFERENCES ugc.assignment(assignment_id)
```

#### Отличия signals.ride_track_point

`no diff`

#### Этап 1: изменения в БД и libdb

```SQL
ALTER TABLE signals.track_point
    ADD COLUMN assignment_id bigint REFERENCES ugc.assignment(assignment_id);
```

```SQL
CREATE INDEX CONCURRENTLY IF NOT EXISTS track_point_assignment_id_index
    ON signals.track_point(assignment_id)
    WHERE assignment_id IS NOT NULL;
```

```SQL
CREATE INDEX CONCURRENTLY IF NOT EXISTS ride_track_point_assignment_id_index
    ON signals.ride_track_point(assignment_id)
    WHERE assignment_id IS NOT NULL;
```

```C++
class TrackPoint {
+    std::optional<TId> assignmentId_;
};

class AssignmentTrackPoint {
-    TId assignmentId_;
};

struct table::TrackPointBase {
+    static constexpr NullableNumericColumn<TId> assignmentId{"assignment_id"sv, name_};
};

struct table::AssignmentTrackPoint {
-    static constexpr NumericColumn<TId> assignmentId{"assignment_id"sv, name_};
};
```

#### Этап 2: select/update только через базовую таблицу

##### Изменения в lt/async_takeout_uploader

```C++
-db::RideTrackPointGateway{*txn};
+db::TrackPointGateway{*txn};
```

##### Изменения в lt/image_inspector

```C++
-db::AssignmentTrackPointGateway{*txn};
+db::TrackPointGateway{*txn};
```

#### Этап 3: insert только в базовую таблицу (agent-proxy)

```C++
-db::AssignmentTrackPointGateway{*txn};
-db::RideTrackPointGateway{*txn};
+db::TrackPointGateway{*txn};
```

#### Этап 4: перенос данных в базовую таблицу

```SQL
WITH deleted AS (
    DELETE FROM ONLY signals.assignment_track_point 
    WHERE id IN (...)
    RETURNING *
)
INSERT INTO signals.track_point(
    accuracy,
    assignment_id,
    date,
    heading,
    id,
    is_augmented
    pos,
    source_id,
    speed
)
SELECT
    accuracy,
    assignment_id,
    date,
    heading,
    id,
    is_augmented
    pos,
    source_id,
    speed
FROM deleted;
```

```SQL
-- signals.ride_track_point 
```

#### Этап 5: удаление таблиц-наследников

```SQL
ALTER TABLE signals.assignment_track_point NO INHERIT signals.track_point;
DROP TABLE signals.assignment_track_point;
```

```SQL
-- signals.ride_track_point
```
