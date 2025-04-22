## Description
This library allows to run [OpenSfM](https://a.yandex-team.ru/arc/trunk/arcadia/contrib/python/opensfm) over YT. OpenSfM is an open source library for [structure from motion](https://en.wikipedia.org/wiki/Structure_from_motion) problem. It takes a set of photos of the same scene and builds its 3D reconstruction. In process it also refines positions and directions of cameras.

## Usage
### Run pipeline
```
~/arcadia/maps/opensfm/common/bin$ ./run_opensfm --yt-dir //path/to/dir/ run_all --input-data dataset_table
```

Result of each pipeline stage (see below) will be stored in tables with names dataset_table_*stage_output* (for example, `dataset_table_matches`) in the specified yt directory.

##### Pipeline results

* dataset_table_gps -- table with refined camera positions and directions
* dataset_table_reconstruction_meshed -- table with 3D reconstructions


### Run certain pipeline stage
##### Example:
```
./run_opensfm --yt-dir //path/to/dir/ match_features --input-features dataset_table_features --output-matches dataset_table_matches
```

### Stages

#### extract_metadata
Extract image metadata and camera parameters from image file.

inputs:

* data

output:

* exif

#### detect_features
Detect features (key points) on image. Feature type and other parameters are defined in opensfm [default config](https://a.yandex-team.ru/arc/trunk/arcadia/contrib/python/opensfm/opensfm/config.py) and can be redefined in [config](bin/config.py).

inputs:

* exif

output:

* features

#### match_features
Match features between image pairs. To reduce amount of matching candidates use 'matching_gps_distance' and 'matching_gps_neighbours' parameters in [config](bin/config.py).

inputs:

* features

output:

* matches

#### create_tracks
Create tracks of key points seen from different images. Result is a bipartite graph with images and track points as nodes, connected when a point is seen from an image.

inputs:

* exif
* features
* matches

output:

* tracks

#### reconstruct
Run incremental reconstruction algorithm on tracks graph.

inputs:

* tracks

output:

* reconstruction

#### mesh
Triangulate reconstruction shots and filter out collapsed shots.

inputs:

* tracks
* reconstruction

output:

* reconstruction-meshed

#### export_gps
Extract refined gps and shot direction from reconstruction.

inputs:

* reconstruction-meshed

output:

* gps
