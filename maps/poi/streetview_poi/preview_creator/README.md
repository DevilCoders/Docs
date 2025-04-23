### Binary for creating panoramas screenshots

* You need `yandex-maps-streetview-description` dataset
* Run command looks like:
```
./prepare_streetview_pics --width 256 --height 256 --pano-index-dir $DATASET_DIR --input-table //home/maps/users/mlevkov/poi_streetview/sample --output-table //home/maps/users/mlevkov/poi_streetview/output --threads 3
```
