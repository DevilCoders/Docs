## Description
Given images and sign detections tables this pipeline finds positions of detected signs via [OpenSfM](https://a.yandex-team.ru/arc/trunk/arcadia/contrib/python/opensfm). It uses [OpenSFM over YT](https://a.yandex-team.ru/arc/trunk/arcadia/maps/opensfm/opensfm_over_yt) implementation with additional feature adding stage and than searches for signs using the reconstructed positions of matched points (see [OpenSfM](https://a.yandex-team.ru/arc/trunk/arcadia/contrib/python/opensfm) description for more details) 

## Usage
### Run pipeline
```
./detections_to_gps --yt-dir //path/to/dir/ run_all --input-data dataset_table --input-detections detections_table
```
There `dataset_table` can be the result of [interpolate_tracks](https://a.yandex-team.ru/arc/trunk/arcadia/maps/opensfm/road_signs/interpolate_tracks) script, and `detections_table` is the result of [sign_detection](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/tools/sign_detection_yt) script. 

Result of each pipeline stage (see below) will be stored in tables with names dataset_table_detections_*stage_output* (for example, `dataset_table_detections_matches`) in the specified yt directory.

##### Pipeline results

* `dataset_table_detections_gps_reduced` -- table with reconstructed sign positions (as lla coordinates), sign types and some additional information

### Run certain pipeline stage
##### Example:
```
./detections_to_gps --yt-dir //path/to/dir/ detections_to_matches --input-features dataset_table_features --input-detections dataset_table_detections --output-detections-matches dataset_table_detections_matches
```

### Stages

#### add_sign_points
This stage is used after `detect_features` stage of OpenSFM in order to add points with special descriptors to each sign detection (see documentation for further details)

inputs:

* features

output:

* features

#### detections_to_matches
Uses bounding boxes of detections and finds the feature-points (from `dataset_table_features`) located in this bb, thus
obtaining feature_id of point that belongs to sign

inputs:

* features, detections

output:

* detections_matches

#### detections_to_tracks
Joins `track_ids` to previous table using `image_id` and `feature_id` (there `image_id` is `feature_id` from `dataset_table`, and `feature_id` is position of feature in feature array from `dataset_table_features`)

inputs:

* tracks, detections_matches

output:

* detections_tracks

#### group_detections
Groups `track_ids` by graph which is constructed as follows: its vertices are `track_ids` and edge is added between two vertices that occur on the same detection. Additionally it joins `track_ids` with different `grid_pos_hash` (see documentation for further details). The result is `group_id` field

inputs:

* detections_tracks

output:

* detections_tracks_grouped

#### detections_to_gps
Adds reconstructed positions as lla coordinates to track_ids

inputs:

* reconstruction_meshed, detections_tracks_grouped

output:

* detections_gps_grouped

#### group_reduce
Transforms groups of tracks into signs using `group_id` and DBSCAN to deal with some special cases

inputs:

* detections_gps_grouped

output:

* detections_gps_reduced
