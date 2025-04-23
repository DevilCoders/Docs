Task Tariff Map
===============
Calculates `task_tariff_map` dictionaries.

Tariffs dictionaries are generated from [tariffs description][tariffs] and stored on Hahn YT cluster.

There are different tariff types. Supported tariff types can be obtained by `--help` command line argument. Tariff type is selected by `--tariff-type` command line argument.

Dictionaries for each tariff type are put into corresponding directories. The list of directories can be obtained by `--help` command line argument.
The default directory can be overriden by `--out-yt-dir` command line argument.

Tariffs differ from date to date. By default, tariffs for today are generated. Tariffs for a particular date are calculated by means of command line argument `--date`.

Tariffs for a period of time can be easily calculated by means of the following bash-script, for example tariffs from 2019-12-25 to 2020-01-07 (both dates inclusive):

    tariff_type=cartographic
    start_date=2019-12-25
    end_date=2020-01-07
    while ! [[ $start_date > $end_date ]]; do
        echo $start_date
        ./task_tariff_map --tariff-type $tariff_type --date $start_date
        start_date=$(date -d "$start_date + 1 day" +%F)
    done


[tariffs]: /arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/dictionaries/tariff
