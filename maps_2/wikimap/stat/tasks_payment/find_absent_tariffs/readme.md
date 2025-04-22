Find Absent Tariffs
===================
Prints tariffs used in logs but absent in `task_tariff_map` dictionary for the provided date.


Usage
-----
Command line arguments:
* `--date <date>` - the date (YYYY-MM-DD) absent tariffs must be looked for.
* `--task-tariff-map-dir <dir>` - YT directory with `task_tariff_map` dictionaries.
* `--log-dirs <dir> ...` - one or more YT directories with logs.

Usage example:

    ./find_absent_tariffs\
        --date 2021-08-19\
        --task-tariff-map-dir //home/maps/core/nmaps/analytics/tasks_payment/dictionaries/task_tariff_map\
        --log-dirs\
            //home/maps/core/nmaps/analytics/tasks_payment/tasks_logs/assessment_log\
            //home/maps/core/nmaps/analytics/tasks_payment/tasks_logs/autocart_log\
            //home/maps/core/nmaps/analytics/tasks_payment/tasks_logs/feedback_log\
            //home/maps/core/nmaps/analytics/tasks_payment/tasks_logs/moderation_log\
            //home/maps/core/nmaps/analytics/tasks_payment/tasks_logs/outsource_log\
            //home/maps/core/nmaps/analytics/tasks_payment/tasks_logs/tracker_log
