# Extractor tool

Tool for building a ymapsdf region by extracting data from original ymapsdf region in desired bounding box.
Resulting region can be passed to road_graph_import_yt, which will build road graph yt tables from it.

### Usage example
```
./extract -i //home/maps/core/garden/stable/ymapsdf/latest/cis1 -o <path_to_result> --minx=37.141180 --miny=55.523804 --maxx=37.904687 --maxy=55.934988 --verbose
```
