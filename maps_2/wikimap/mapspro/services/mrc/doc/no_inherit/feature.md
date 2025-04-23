### Иерархия signals.feature

#### Отличия signals.feature

```
Check constraints:
    "feature_heading_null_check" CHECK (heading IS NOT NULL) NO INHERIT
    "feature_pos_null_check" CHECK (pos IS NOT NULL) NO INHERIT
```

#### Отличия signals.assignment_photo

| Column        | Type   | Nullable |
| ------------- | ------ | -------- |
| assignment_id | bigint | not null |

```
Indexes:
    "assignment_photo_assignment_id_camera_deviation_index" btree (assignment_id, camera_deviation, date) -- not used
    "assignment_photo_assignment_id_id_index" btree (assignment_id, feature_id) -- not used
    "assignment_photo_assignment_id_index" btree (assignment_id)
Foreign-key constraints:
    "assignment_photo_assignment_id_fkey" FOREIGN KEY (assignment_id) REFERENCES ugc.assignment(assignment_id)
```

#### Отличия signals.ride_photo

| Column          | Type    | Nullable |
| --------------- | ------- | -------- |
| user_id         | text    | not null |
| gdpr_deleted    | boolean |          |
| show_authorship | boolean |          |
| deleted_by_user | boolean |          |

```
Indexes:
    "ride_photo_should_be_published_deleted_by_user_idx" btree (should_be_published, deleted_by_user) WHERE should_be_published AND deleted_by_user -- will not used
    "ride_photo_user_id_date_idx" btree (user_id, date)
    "ride_photo_user_id_gdpr_deleted_idx" btree (user_id, gdpr_deleted)
Referenced by:
    TABLE "rides.queued_photo_id" CONSTRAINT "queued_photo_id_photo_id_fkey" FOREIGN KEY (photo_id) REFERENCES signals.ride_photo(feature_id) ON DELETE CASCADE
```

#### Отличия signals.walk_photo

| Column          | Type             | Nullable |
| --------------- | ---------------- | -------- |
| user_id         | text             | not null |
| gdpr_deleted    | boolean          |          |
| walk_object_id  | bigint           | not null |

```
Indexes:
    "walk_photo_user_id_date_idx" btree (user_id, date)
    "walk_photo_user_id_gdpr_deleted_idx" btree (user_id, gdpr_deleted)
    "walk_photo_walk_object_index" btree (walk_object_id)
Foreign-key constraints:
    "walk_photo_walk_object_id_fkey" FOREIGN KEY (walk_object_id) REFERENCES signals.walk_object(id)
```

#### Этап 1: изменения в БД и libdb

```SQL
ALTER TABLE signals.feature
    DROP CONSTRAINT IF EXISTS feature_heading_null_check,
    DROP CONSTRAINT IF EXISTS feature_pos_null_check,
    ADD COLUMN assignment_id bigint REFERENCES ugc.assignment(assignment_id),
    ADD COLUMN user_id text,
    ADD COLUMN gdpr_deleted boolean,
    ADD COLUMN show_authorship boolean,
    ADD COLUMN deleted_by_user boolean,
    ADD COLUMN walk_object_id bigint REFERENCES signals.walk_object(id);

ALTER TABLE rides.queued_photo_id
    DROP CONSTRAINT IF EXISTS queued_photo_id_photo_id_fkey;
```

```SQL
CREATE INDEX CONCURRENTLY IF NOT EXISTS feature_assignment_id_index
    ON signals.feature(assignment_id)
    WHERE assignment_id IS NOT NULL;
```

```SQL
CREATE INDEX CONCURRENTLY IF NOT EXISTS ride_photo_assignment_id_index
    ON signals.ride_photo(assignment_id)
    WHERE assignment_id IS NOT NULL;
```

```SQL
CREATE INDEX CONCURRENTLY IF NOT EXISTS walk_photo_assignment_id_index
    ON signals.walk_photo(assignment_id)
    WHERE assignment_id IS NOT NULL;
```

```SQL
CREATE INDEX CONCURRENTLY IF NOT EXISTS feature_user_id_date_index
    ON signals.feature (user_id, date);
    WHERE user_id IS NOT NULL;
```

```SQL
CREATE INDEX CONCURRENTLY IF NOT EXISTS assignment_photo_user_id_date_index
    ON signals.assignment_photo (user_id, date);
    WHERE user_id IS NOT NULL;
```

```SQL
CREATE INDEX CONCURRENTLY IF NOT EXISTS feature_user_id_gdpr_deleted_index
    ON signals.feature (user_id, gdpr_deleted);
    WHERE user_id IS NOT NULL;
```

```SQL
CREATE INDEX CONCURRENTLY IF NOT EXISTS assignment_photo_user_id_gdpr_deleted_index
    ON signals.assignment_photo (user_id, gdpr_deleted);
    WHERE user_id IS NOT NULL;
```

```SQL
CREATE INDEX CONCURRENTLY IF NOT EXISTS feature_walk_object_index
    ON signals.feature (walk_object_id)
    WHERE walk_object_id IS NOT NULL;
```

```SQL
CREATE INDEX CONCURRENTLY IF NOT EXISTS assignment_photo_walk_object_index
    ON signals.assignment_photo (walk_object_id)
    WHERE walk_object_id IS NOT NULL;
```

```SQL
CREATE INDEX CONCURRENTLY IF NOT EXISTS ride_photo_walk_object_index
    ON signals.ride_photo (walk_object_id)
    WHERE walk_object_id IS NOT NULL;
```

```C++
class Feature {
+    std::optional<TId> assignmentId_;
+    std::optional<std::string> userId_;
+    std::optional<bool> gdprDeleted_;
+    std::optional<bool> showAuthorship_;
+    std::optional<bool> deletedByUser_;
+    std::optional<TId> walkObjectId_;
};

class AssignmentPhoto {
-    TId assignmentId_;
};

class RidePhoto {
-    std::string userId_;
-    std::optional<bool> gdprDeleted_;
-    std::optional<bool> showAuthorship_;
-    std::optional<bool> deletedByUser_;
};

class WalkPhoto {
-    std::string userId_;
-    std::optional<bool> gdprDeleted_;
-    std::optional<double> accuracy_;
-    TId walkObjectId_;
};

struct table::FeatureBase {
+    static constexpr NullableNumericColumn<TId> assignmentId{"assignment_id"sv, name_};
+    static constexpr NullableStringColumn userId{"user_id"sv, name_};
+    static constexpr NullableBooleanColumn gdprDeleted{"gdpr_deleted"sv, name_};
+    static constexpr NullableBooleanColumn showAuthorship{"show_authorship"sv, name_};
+    static constexpr NullableBooleanColumn deletedByUser{"deleted_by_user"sv, name_};
+    static constexpr NullableNumericColumn<TId> walkObjectId{"walk_object_id"sv, name_};
};

struct table::AssignmentPhoto {
-    static constexpr NumericColumn<TId> assignmentId{"assignment_id"sv, name_};
};

struct table::RidePhoto {
-    static constexpr StringColumn userId{"user_id"sv, name_};
-    static constexpr NullableBooleanColumn gdprDeleted{"gdpr_deleted"sv, name_};
-    static constexpr NullableBooleanColumn showAuthorship{"show_authorship"sv, name_};
-    static constexpr NullableBooleanColumn deletedByUser{"deleted_by_user"sv, name_};
};

struct table::WalkPhoto {
-    static constexpr StringColumn userId{"user_id"sv, name_};
-    static constexpr NullableDoubleColumn accuracy{"accuracy"sv, name_};
-    static constexpr NullableBooleanColumn gdprDeleted{"gdpr_deleted"sv, name_};
-    static constexpr NumericColumn<TId> walkObjectId{"walk_object_id"sv, name_};
};

```

#### Этап 2: select/update только через базовую таблицу

##### Изменения в browser

```C++
-db::RidePhotoGateway{*txn};
-db::WalkPhotoGateway{*txn};
+db::FeatureGateway{*txn};
```

##### Изменения в lt/assignment_object_feedback_tasks_emitter

```C++
-db::AssignmentPhotoGateway{*txn};
+db::FeatureGateway{*txn};
```

##### Изменения в lt/async_ride_correction

```C++
-db::RidePhotoGateway{*txn};
+db::FeatureGateway{*txn};
```

##### Изменения в lt/async_takeout_data_erasure

```C++
-db::RidePhotoGateway{*txn};
-db::WalkPhotoGateway{*txn};
+db::FeatureGateway{*txn};
```

##### Изменения в lt/async_takeout_uploader

```C++
-db::table::RidePhoto
-db::table::WalkPhoto
+db::table::FeatureBase
```

##### Изменения в lt/export_gen

```C++
-db::RidePhotoGateway{*txn};
-db::WalkPhotoGateway{*txn};
+db::FeatureGateway{*txn};
```

##### Изменения в lt/image_inspector

```C++
-db::AssignmentPhotoGateway{*txn};
+db::FeatureGateway{*txn};
```

##### Изменения в lt/regular_upload

```C++
-db::table::AssignmentPhoto
-db::table::RidePhoto
-db::table::WalkPhoto
+db::table::FeatureBase
```

##### Изменения в lt/ride_inspector

```C++
-db::RidePhotoGateway{*txn};
+db::FeatureGateway{*txn};
```

##### Изменения в lt/ugc_uploader

```C++
-db::RidePhotoGateway{*txn};
+db::FeatureGateway{*txn};
```

##### Изменения в lt/user_activity_stat

```C++
-db::table::RidePhoto
+db::table::FeatureBase
```

##### Изменения в lt/yt_features_exporter

```C++
-db::table::AssignmentPhoto
+db::table::FeatureBase
```

##### Изменения в onfoot-processor

```C++
-db::WalkPhotoGateway{*txn};
+db::FeatureGateway{*txn};
```

##### Изменения в tasks-planner

```C++
-db::AssignmentPhotoGateway{*txn};
-db::RidePhotoGateway{*txn};
-db::WalkPhotoGateway{*txn};
+db::FeatureGateway{*txn};
```

##### Изменения в ugc_back

```C++
-db::RidePhotoGateway{*txn};
+db::FeatureGateway{*txn};
```

#### Этап 3: insert только в базовую таблицу (agent-proxy)

```C++
-db::AssignmentPhotoGateway{*txn};
-db::RidePhotoGateway{*txn};
-db::WalkPhotoGateway{*txn};
+db::FeatureGateway{*txn};
```

#### Этап 4: перенос данных в базовую таблицу

```SQL
DROP TRIGGER IF EXISTS delete_house_number_feature_on_feature_deletion ON signals.feature;
DROP TRIGGER IF EXISTS delete_house_number_feature_on_feature_deletion ON signals.assignment_photo;
DROP TRIGGER IF EXISTS delete_house_number_feature_on_feature_deletion ON signals.ride_photo;
DROP TRIGGER IF EXISTS delete_house_number_feature_on_feature_deletion ON signals.walk_photo;

DROP TRIGGER IF EXISTS delete_object_in_photo_on_feature_deletion ON signals.feature;
DROP TRIGGER IF EXISTS delete_object_in_photo_on_feature_deletion ON signals.assignment_photo;
DROP TRIGGER IF EXISTS delete_object_in_photo_on_feature_deletion ON signals.ride_photo;

DROP TRIGGER IF EXISTS delete_sign_feature_on_feature_deletion ON signals.feature;
DROP TRIGGER IF EXISTS delete_sign_feature_on_feature_deletion ON signals.assignment_photo;
DROP TRIGGER IF EXISTS delete_sign_feature_on_feature_deletion ON signals.ride_photo;
DROP TRIGGER IF EXISTS delete_sign_feature_on_feature_deletion ON signals.walk_photo;

DROP TRIGGER IF EXISTS delete_traffic_light_feature_on_feature_deletion ON signals.feature;
DROP TRIGGER IF EXISTS delete_traffic_light_feature_on_feature_deletion ON signals.assignment_photo;
DROP TRIGGER IF EXISTS delete_traffic_light_feature_on_feature_deletion ON signals.ride_photo;
DROP TRIGGER IF EXISTS delete_traffic_light_feature_on_feature_deletion ON signals.walk_photo;
```

```SQL
WITH deleted AS (
    DELETE FROM ONLY signals.assignment_photo 
    WHERE feature_id IN (...)
    RETURNING *
)
INSERT INTO signals.feature(
    assignment_id,
    camera_deviation,
    camera_orientation_rodrigues,
    dataset,
    date,
    deleted_by_user,
    feature_id,
    forbidden_probability,
    gdpr_deleted,
    graph,
    heading,
    height,
    is_published,
    mds_group_id,
    mds_path,
    moderators_should_be_published,
    odometer_pos,
    orientation,
    pos,
    privacy,
    quality,
    road_probability,
    should_be_published,
    show_authorship,
    source_id,
    uploaded_at,
    user_id,
    walk_object_id,
    width
)
SELECT
    assignment_id,
    camera_deviation,
    camera_orientation_rodrigues,
    dataset,
    date,
    deleted_by_user,
    feature_id,
    forbidden_probability,
    gdpr_deleted,
    graph,
    heading,
    height,
    is_published,
    mds_group_id,
    mds_path,
    moderators_should_be_published,
    odometer_pos,
    orientation,
    pos,
    privacy,
    quality,
    road_probability,
    should_be_published,
    show_authorship,
    source_id,
    uploaded_at,
    user_id,
    walk_object_id,
    width
FROM deleted;
```

```SQL
-- signals.ride_photo 
```

```SQL
-- signals.walk_photo 
```

#### Этап 5: удаление таблиц-наследников, восстановление связей

```SQL
ALTER TABLE signals.assignment_photo NO INHERIT signals.feature;
DROP TABLE signals.assignment_photo;
```

```SQL
-- signals.ride_photo
```

```SQL
-- signals.walk_photo
```

```SQL
ALTER TABLE eye.feature_to_frame 
    ADD CONSTRAINT feature_to_frame_feature_id_fkey
    FOREIGN KEY (feature_id) 
    REFERENCES signals.feature (feature_id)
    NOT VALID;
```

```SQL
ALTER TABLE eye.feature_to_frame
    VALIDATE CONSTRAINT feature_to_frame_feature_id_fkey;
```

```SQL
ALTER TABLE house.house_number_feature 
    ADD CONSTRAINT house_number_feature_feature_id_fkey
    FOREIGN KEY (feature_id) 
    REFERENCES signals.feature (feature_id)
    NOT VALID;
```

```SQL
ALTER TABLE house.house_number_feature
    VALIDATE CONSTRAINT house_number_feature_feature_id_fkey;
```

```SQL
ALTER TABLE rides.queued_photo_id 
    ADD CONSTRAINT queued_photo_id_photo_id_fkey
    FOREIGN KEY (photo_id) 
    REFERENCES signals.feature (feature_id)
    NOT VALID;
```

```SQL
ALTER TABLE rides.queued_photo_id
    VALIDATE CONSTRAINT queued_photo_id_photo_id_fkey;
```

```SQL
ALTER TABLE signals.object_in_photo
    ADD CONSTRAINT object_in_photo_feature_id_fkey
    FOREIGN KEY (feature_id) 
    REFERENCES signals.feature (feature_id)
    NOT VALID;
```

```SQL
ALTER TABLE signals.object_in_photo
    VALIDATE CONSTRAINT object_in_photo_feature_id_fkey;
```

```SQL
ALTER TABLE signs_detect.sign_feature
    ADD CONSTRAINT sign_feature_feature_id_fkey
    FOREIGN KEY (feature_id) 
    REFERENCES signals.feature (feature_id)
    NOT VALID;
```

```SQL
ALTER TABLE signs_detect.sign_feature
    VALIDATE CONSTRAINT sign_feature_feature_id_fkey;
```

```SQL
ALTER TABLE traffic_light.traffic_light_feature
    ADD CONSTRAINT traffic_light_feature_feature_id_fkey
    FOREIGN KEY (feature_id) 
    REFERENCES signals.feature (feature_id)
    NOT VALID;
```

```SQL
ALTER TABLE traffic_light.traffic_light_feature
    VALIDATE CONSTRAINT traffic_light_feature_feature_id_fkey;
```
