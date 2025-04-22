# Road graph import yt

Library for importing road graph tables from yamapsdf tables using mr-paradigm

### Usage example
* ```bash
  yt list //home/maps/core/garden/stable/ymapsdf/latest | tr '\n' ' ' | sed -e 's/\([^ ][^ ]*\)/-r \/\/home\/garden\/prod\/ymapsdf\/latest\/\1/g' | xargs -I{} sh -c './bin/road_graph_import_yt -c hahn {} -a auto -v -o $OUTPUT_GRAPH_DIR'
  ```
* ```bash
  echo 'cis1 cis2 eu1 eu3 eu4 na saa tr' | sed -e 's/\([^ ][^ ]*\)/-r \/\/home\/garden\/prod\/ymapsdf\/latest\/\1/g' | xargs -I{} sh -c './bin/road_graph_import_yt -c hahn {} -a auto -v -o $OUTPUT_GRAPH_DIR'
  ```
