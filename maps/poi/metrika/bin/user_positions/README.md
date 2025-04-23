### Binary for retrieving daily user positions from AppMetrika

#### Description

The main daily Metrika export can be found in [//home/logfeller/logs/metrika-mobile-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/metrika-mobile-log/1d).  
Daily Metrika tables with coordinates can be found in [//logs/appmetrica-location-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//logs/appmetrica-location-log/1d).

#### Parameters

* `--date` - the date (YY-MM-DD) for which the positions should be retrieved
* `--output-dir` - YT-directory with daily tables

* Usage example:
```
./user_positions --date 2020-09-01 --output-dir //home/maps/poi/data/metrika/user_positions
```

#### Results

Output table contains the following fields:
- `AccountID` - user passport id
- `EventTimestamp` - event time in UNIX format
- `Longitude` - user's longitude
- `Latitude` - user's latitude
