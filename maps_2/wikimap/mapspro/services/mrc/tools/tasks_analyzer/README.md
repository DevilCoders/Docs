Compares actual and planned route for tasks. Saves results to easyview files.

```
quoter@pollux:~/devel/arcadia/maps/wikimap/mapspro/services/mrc/tools/tasks_analyzer$ ./tasks_analyzer --config ../../libs/common/cfg/config.testing.xml --task 3138 --easyview task_3138.ev
[2018-04-11 14:14:17] <tasks_analyzer 295363> info: pgpool.core.pool created with configuration:
[2018-04-11 14:14:18] <tasks_analyzer 295363> info: pgpool.core.pool new configuration: mrc-pg01h.tst.cloud.maps.yandex.net:5432: M offline: not pinged yet
[2018-04-11 14:14:18] <tasks_analyzer 295363> info: pgpool.core.ctrl configuration replaced, Last-Modified=[Unknown], Id=[d4ae130a057326df3584ede62f5ec9a7]
[2018-04-11 14:14:19] <tasks_analyzer 295363> info: pgpool.core.pool instance mrc-pg01h.tst.cloud.maps.yandex.net:5432 became ONLINE: M online: 2a02:6b8:0:1a71::3728: 1.07454s
[2018-04-11 14:14:22] <tasks_analyzer 295363> info: pgpool.core.pool.get_slave_#0 created connection #0 to mrc-pg01h.tst.cloud.maps.yandex.net:5432 connstr='host=2a02:6b8:0:1a71::3728 port=5432 dbname=mrc user=mrc password=QPDfcvN5K'
[2018-04-11 14:14:30] <tasks_analyzer 295363> info: processing task id=3138 MoscowWO8 Москва_98
[2018-04-11 14:14:43] <tasks_analyzer 295363> info: Total targets length: 72836.1 meters
[2018-04-11 14:14:43] <tasks_analyzer 295363> info: Total route length: 116659 meters
[2018-04-11 14:14:43] <tasks_analyzer 295363> info: Ratio is 1.60166
[2018-04-11 14:14:43] <tasks_analyzer 295363> info: good: 1 routes 29.7804 m
[2018-04-11 14:14:43] <tasks_analyzer 295363> info: bad: 1218 routes 116612 m
[2018-04-11 14:14:44] <tasks_analyzer 295363> info: From 37.5638 55.571 to 37.5635 55.5707 distance increase for 976.996
[2018-04-11 14:14:44] <tasks_analyzer 295363> info: From 37.5768 55.5656 to 37.5775 55.5651 distance increase for 996.53
[2018-04-11 14:14:44] <tasks_analyzer 295363> info: From 37.5901 55.568 to 37.5905 55.5683 distance increase for 2756
[2018-04-11 14:14:44] <tasks_analyzer 295363> info: From 37.5934 55.5712 to 37.5928 55.5718 distance increase for 2545.35
[2018-04-11 14:14:44] <tasks_analyzer 295363> info: From 37.5921 55.5757 to 37.5919 55.5757 distance increase for 2462.12
[2018-04-11 14:14:44] <tasks_analyzer 295363> info: From 37.5919 55.5757 to 37.591 55.5759 distance increase for 5283.07
[2018-04-11 14:14:44] <tasks_analyzer 295363> info: From 37.5749 55.5787 to 37.5757 55.5785 distance increase for 1059.99
[2018-04-11 14:14:45] <tasks_analyzer 295363> info: From 37.5736 55.579 to 37.5729 55.5793 distance increase for 2241.97
[2018-04-11 14:14:45] <tasks_analyzer 295363> info: From 37.5927 55.5696 to 37.5928 55.5695 distance increase for 940.926
[2018-04-11 14:14:45] <tasks_analyzer 295363> info: From 37.5905 55.5683 to 37.5905 55.5681 distance increase for 2543.17
[2018-04-11 14:14:45] <tasks_analyzer 295363> warning: actual route does not contain 37.5558 55.5849 distance is 12.3257
[2018-04-11 14:14:45] <tasks_analyzer 295363> warning: actual route does not contain 37.5555 55.5848 distance is 22.9463
[2018-04-11 14:14:45] <tasks_analyzer 295363> warning: actual route does not contain 37.5555 55.5848 distance is 26.3447
[2018-04-11 14:14:45] <tasks_analyzer 295363> warning: actual route does not contain 37.5559 55.5848 distance is 12.2727
[2018-04-11 14:14:45] <tasks_analyzer 295363> info: From 37.5717 55.5787 to 37.5708 55.578 distance increase for 7715.6
[2018-04-11 14:14:46] <tasks_analyzer 295363> info: From 37.5706 55.5622 to 37.5709 55.5621 distance increase for 2662.22
[2018-04-11 14:14:46] <tasks_analyzer 295363> info: From 37.578 55.5649 to 37.578 55.5648 distance increase for 729.998
[2018-04-11 14:14:46] <tasks_analyzer 295363> info: From 37.5856 55.559 to 37.5852 55.5594 distance increase for 1049.83
[2018-04-11 14:14:46] <tasks_analyzer 295363> warning: actual route does not contain 37.5593 55.5532 distance is 4.00428
[2018-04-11 14:14:46] <tasks_analyzer 295363> warning: actual route does not contain 37.5609 55.5526 distance is 6.94034
[2018-04-11 14:14:46] <tasks_analyzer 295363> warning: actual route does not contain 37.5613 55.5526 distance is 23.6176
[2018-04-11 14:14:46] <tasks_analyzer 295363> warning: actual route does not contain 37.5615 55.5524 distance is 6.60065
[2018-04-11 14:14:46] <tasks_analyzer 295363> info: From 37.5611 55.5525 to 37.5606 55.5527 distance increase for 566.216
[2018-04-11 14:14:46] <tasks_analyzer 295363> info: From 37.5599 55.553 to 37.5594 55.5533 distance increase for 7672.21
[2018-04-11 14:14:46] <tasks_analyzer 295363> info: From 37.5872 55.5613 to 37.5884 55.5608 distance increase for 1954.43

```