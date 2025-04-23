## Description
Scripts to calculate solver uptime, save it into DB and send status to Juggler.
Contains two stages:
1) monitoring -- sends tasks to Solver, get result and saves status and timings into the DB
2) uptime -- processes data from the previous step, saves it into the DB, sends status to Juggler.

## Usage
### monitoring
`./monitoring --apikey=... --task-size=small --matrix-router=main --solver-instance=RTC_STABLE --env=stable --log-path=monitoring.log`

Sends tasks to Solver and saves the result into table 'uptime.monitoring':
  * `--task-size` -- type of tasks
  * `--matrix-router -- type of matrix router
  * `--solver-instance` -- Solver installation: RTC_STABLE (default), RTC_TESTING, ...
  * `--env` -- script and DB environment, if useful for develompent

### uptime
`uptime --date 2022-04-05 --solver-instance RTC_STABLE --env stable --juggler --log-path uptime.log`

Reads results from table 'uptime.monitoring', calculates uptime and saves it into tables 'uptime.uptime', 'uptime.uptime_daily'.
  * `--date` -- process data for the specified date
  * `--juggler` -- send status to Juggler

Other parameters -- see the previous script.
