# The tool generates clusters for users end-track and wait points

It gets data from the following tables

```//home/statistics-navi/production/event_log/{date}```

```//statbox/analyzer-dispatcher-signals-log/{date}```

and stores results into

```//home/maps/carparks/production/daps/mined```

table.

Sandbox tasks:

* [Testing](https://sandbox.yandex-team.ru/scheduler/20039/view)

* [Production](https://sandbox.yandex-team.ru/scheduler/11390/view)

How to test:

* Go to http://maps-mobgeoplatform-dev.man.yp-c.yandex.net:10001/daps/
* Enter target address in the top left corner input field


Main scenario is listed below.

1) From metrika table we generate daily suggested_points_table:
    metrika -> raw_table -> enhanced_table -> suggested_points_table.

2) Geocode list of suggested_points tables. Produce 
geocoded_suggested_points_cache and geocoded_suggested_points_errors.
In this two tables we store results of address geocoding.
All rows from suggested_points tables inserted into: 
- geocoded_suggested_points: points with geocoder or organization id
- geocoded_suggested_points_dropout: points droped out by distance (too far)

3) From old filtered_points_id and geocoded_suggested_points tables generate 
new filtered_points_id table

4) From new filtered_points_id table generate clusters and store them into clusterized_points_table.

## Usage

```bash
./carparks_miner <Path to the config>
```

Path can be like this:

```bash
/arc/trunk/arcadia/maps/carparks/tools/carparks_miner/config/carparks_miner.production.json
```

The following config parameters are required:

* "yt_root": "//home/maps/carparks/production/daps/mined/"

* "yt_carparks_dataset": "//home/maps/core/garden/stable/carparks/datasets/yandex-maps-carparks-handler-data/LATEST"

Additionally you may specify the following optional parameters:
* "clusterize_reducer_spec"

* "geocode_reducer_spec"

* "begin_date": "YYYY-MM-DD"

* "end_date": "YYYY-MM-DD"

* "regions": [1, 2]

And we want to run testing on limited set of regions, for example [20279, 20360, 103728, 120911]:

* 20279 - The Central Administrative District of Moscow

* 20360 - Southern Administrative District of Moscow

* 103728 - Istanbul

* 120911 - Nizhny Novgorod Urban Okrug

## Cleaner

[Script for data cleaning](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/carparks/tools/cleaner)

## Квота sandbox

[MAPS-CORE-CARPARKS](https://sandbox.yandex-team.ru/admin/groups/MAPS-CORE-CARPARKS/general)
