# Prerequisites
- Arcadia is available
- **Required jams cut is prepared** - yandex-maps-jams-speeds
    Can be downloaded with **dumper.sh** script

# How to use isochrone metrics tool
1. Download ecstatic-datasets for isochrone
    - yandex-maps-graph-compact
    - yandex-maps-graph-compact-edges-persistent-index
    - yandex-maps-graph-compact-rtree
2.  Produce flatbuffer for isochrone
    [Arcadia link](https://a.yandex-team.ru/arc/trunk/arcadia/junk/antonrybakov/jams2realtyjams/cpp)
3.  Patch isochrone configuration file to use files above and run it
4.  Download additional ecstatic-datasets for creation of leptidea patch
    -   yandex-maps-graph-router-topology7
    -   yandex-maps-graph-router-compact-data7
    -   yandex-maps-jams-closures
5.  Create a patch for leptidea using
    [Arcadia Link](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/leptidea/bin/create_data/create_data_patch)
    ```sh
        ./create_data_patch \
          -t <path_to_topology> \
          -g <path_to_road_graph> \
          -i <path_to_persistent_index> \
          -p <path_to_jams_files> \
          --closures <path_to_closures> \
          --base <base_leptidea_data> \
          --fb <output_flatbuffer>
    ```
6.  Download additional ecstatic-datasets for running router
    -   yandex-maps-graph-routing-barriers-rtree
    -   yandex-maps-jams-edge-sequences-statistics
    -   yandex-maps-graph-router-experimental-speeds-diff
    -   yandex-maps-whole-track-model-info
7.  Create router.json configuration file for router
    [Arcadia link to router](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router/yacare/bin)
    Dump default config with:
    ```sh
    ./router --config > router.json
    ```
    And correct coresponding paths to datasets
8.  Run router and call "/reload_jams"
9.  Use isochrone metrics tool for raw csv output
10. Analyze output with table processor or script analyze.py

