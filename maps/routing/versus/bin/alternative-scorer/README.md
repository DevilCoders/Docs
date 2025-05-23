Alternative Scorer
==================

Evaluate routing quality of your local copy of `maps/libs/leptidea`.


Description
-----------

Alternative scorer links against your local copy of `maps/libs/leptidea`
library. Make sure you rebuilt the `alternative-scorer` binary if you wish to
test the latest local changes in leptidea.

Alternative scorer uses YT tables and files generated by [versus](../..),
specifically:
* `etalon_routes`: table with evaluated etalon routes;
* `realtime_routes`: table with evaluated routes built using realtime jams;
* `etalon_jams.mms`: "reversed" binary jams, used to calculate travel times
  along routes.

These items are typically located inside
`//home/maps/users/<user>/versus/<region>/<timeframe>/<graph version>` node on
YT Hahn. This is the path that should be specified with `--yt-path` option.

No items in YT are modified, read-only access is sufficient. No YT operations
are started. You should be able to safely use the items generated by another
user.

Alternative scorer requires you have the following graph files locally
available:
* `road_graph.fb`
* `edges_persistent_index.fb`
* `l6a_topology.fb.7`
* `l6a_data.fb.7`

They should be taken from the same graph version that was used to generate the
YT items. You can use the YT CLI to download them from Hahn:
```
YT_PROXY=hahn yt download //home/maps/graph/<graph_version>/<file> > <file>
```


How to run
----------

1. Find a suitable set of generated items in YT, most likely located at
   `//home/maps/users/<user>/versus/<region>/<timeframe>/<graph version>`. Pay
   attention to the `<timeframe>` component, as you get more accurate results
   with a wider time window. If you cannot find suitable data, generate it
   yourself with the [versus](../..) utility's `prepare-data` script. This
   process takes a long time, and requires requesting some permissions via
   [IDM](https://idm.yandex-team.ru/).

2. If the `<graph version>` is not present on your machine, download the
   required graph files from YT (see **Description** above).

3. Make sure your local copy of `maps/libs/leptidea` contains the version you
   want to test. Build `alternative-scorer`.

4. Run `alternative-scorer`.
   ```
   ./alternative-scorer \
       --yt-path //home/maps/users/<user>/versus/<region>/<timeframe>/<graph version> \
       --graph-path <local directory with graph files> \
       --region <region>
   ```
   To see all options, run `./alternative-scorer` without arguments.

Basic evaluation results are printed to stdout. Some additional information is
written to several [easyview](../../../../tools/easyview)-readable logs for
further investigation. Specifically:
* Queries that etalon dijkstra, leptidea, or both were unable to build routes
  for.
* Queries and routes where leptidea won over etalon route.
