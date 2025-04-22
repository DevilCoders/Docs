## Description
This script takes table with photos and table with tracks (gps information) and interpolates gps information (and, optionally, speed) to photos rows.

## Usage
### Run script
```
./interpolate_tracks --photos-table //path/to/photos/table --tracks-table //path/to/tracks/table --output-path //path/to/store/output --interpolation-type linear --interpolate-speed True
```
One can choose one of two interpolations - linear or spline based. Linear is quite faster, beside that both methods work about equally well. Default method is linear.

##### script inputs

* `--photos-table` -- a table with photos (should have fields `feature_id`, `source_id`, `date` and `image`)

* `--tracks-table` -- a table with tracks (gps information, should have fields `source_id`, `date`, `pos` and, optionally `speed`)

* `--interpolation-type` -- "linear"/"spline", type of interpolation to obtain positions/speeds

* `--interpolate-speed` -- boolean, whether to interpolate speed

##### script results

* `--output-path` -- a table where the results (photos with interpolated positions/speeds) will be saved
