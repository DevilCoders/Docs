## Description
This script takes tables with images and uses [signdetect](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/libs/signdetect) library to detect signs on this images. As a result it generates table with bounding boxes, sign types/categories and confidence

## Usage
### Run script
```
./sign_detection_yt --input-table //path/to/input/table --output-table //path/to/output/table
```

##### script inputs

* `--input-table` -- a table with images

##### script results

* `--output-table` -- a table with bounding boxes (x, y, width, height), sign type, sign category and confidence
