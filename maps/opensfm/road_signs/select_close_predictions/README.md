## Description
This script takes two tables with signs positions predictions and discards some predictions from one table according to closeness of this predictions to ones from other table. This can be used to drop noisy predictions using less noisy method of sign detections

## Usage
### Run script
```
./select_close_predictions --base-predictions-table //path/to/base/predictions/table --new-predictions-table //path/to/new/predictions/table --output-predictions-table /path/to/left/predictions --discarding-distance 10
```

##### script inputs

* `--base-predictions-table` -- a table with baseline predictions

* `--new-predictions-table` -- a table with new predictions. Some of them will be discarded because this predictions located to far from baseline (where "too far" is defined by `--discarding-distance` parameter)

* `--discarding-distance` -- how far should be new prediction from any baseline to be discarded (in meters)

##### script results

* `--output-predictions-table` -- table with predictions that haven't been discarded
