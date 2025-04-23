Tanks shoot at target ymsh01g.load.mobile.yandex.net every workday (start at 2 a.m.). If given result is more than 20% worse that previous one the letter will be sent on taxi-dev@.

Every morning at 8 a.m. database is refilled with the script `/home/dmkurilov/taxi-initial-state/refill_databases.py` which starts from dmkurilov@'s crontab.

There are links to lunapark in every console output of every stable build: http://bmpt.tanks.yandex.net:8080/view/Taxi/job/taxi_metajob_new/

To add new test create new task in startrek, assign it to michurin@ and add r2d2@ to CC.