Schedulers for build Edge Sequence Statistic dataset are located in Sandbox on tab Schedulers. They have type MAPS_BUILD_EDGE_SEQ_STAT:

https://sandbox.yandex-team.ru/schedulers?page=1&pageCapacity=20&order=-id&task_type=MAPS_BUILD_EDGE_SEQ_STAT

Tasks execute hourly.
The task checks input tables have been already created and output dataset has not been uploaded to ecstatic yet. If it so, task will execute build_routes_popularity.

Input:
- Daily travel time table (//home/maps/jams/production/quality-daily/travel_times)
- Daily event log table (//home/statistics-navi/production/event_log)

Output:
    New version of dataset will be uploaded to ecstatic.

The task’s source code: /arc/trunk/arcadia/sandbox/projects/maps/MapsBuildEdgeSeqStat

Warning. If you change the task source code, it will be applied to create testing dataset as well as stable dataset.


For update build_routes_popularity:
- build for Ubuntu 18.04 LTS
    > cd build_routes_popularity
    > ya make -r
- upload to Sandbox:
    > ya upload --type MAPS_EDGE_SEQ_STAT_BUILDER --ttl=inf ./build_routes_popularity
- update parameter “Build edge sequences statistics executable” in Sandbox schedulers.
