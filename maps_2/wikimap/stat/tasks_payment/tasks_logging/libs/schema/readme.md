Cartographic Tasks Logs Format
==============================
Cartographic payment tasks logs format:

    +--------------+------+---------+------------+----------+------+---------+---------+---------+---------+
    | iso_datetime | puid | task_id | mrc_region | quantity | geom | lat_min | lon_min | lat_max | lon_max |
    +--------------+------+---------+------------+----------+------+---------+---------+---------+---------+

Mandatory fields:
* `iso_datetime` - time when the task has been accomplished (in ISO format: `YYYY-MM-DDThh:mm:ss+hh:mm`).
* `puid` - passport uid of the user who did the task.
* `task_id` - a textual task type identifier.
* `quantity` - amount of work done.

Optional fields:
* `mrc_region` - name of mrc region associated with task.
* `geom` - textual hex-encoded EWKB or WKT of the place where the task has been performed.
* `lat_min/max`, `lon_min/max` - [geodetic coordinates][epsg4326] of the `geom` bounding box.

If `geom` field has a value then columns with bounding box coordinates must have values too and vice versa.


GeoTest Tasks Logs Format
=========================
GeoTest payment tasks logs format is very similar to cartographic tasks log format. Though, the log has no geometric columns as testers tasks has no geographic binding. Moreover, staff uids are used instead of passport ones:

    +--------------+-----------+---------+----------+
    | iso_datetime | staff_uid | task_id | quantity |
    +--------------+-----------+---------+----------+

Mandatory fields:
* `iso_datetime` - time when the task has been accomplished (in ISO format: `YYYY-MM-DDThh:mm:ss+hh:mm`).
* `staff_uid` - staff uid of the user who did the task.
* `task_id` - a textual task type identifier.
* `quantity` - amount of work done.


[epsg4326]: https://epsg.io/4326
