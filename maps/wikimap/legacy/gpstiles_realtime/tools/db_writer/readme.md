# gpstiles_realtime db_writer tool
Dev tool for writing realtime GPS signals from requested bbox into postgres DB table:
 - reads signals from LogBroker using `maps/wikimap/gpstiles_realtime/libs/lb_client` library, filters them by region of interest specified in config
 - *Updater* background worker writes new signals received from LogBroker into DB table once in specified update duration
 - *Deleter* background worker deletes signals which age are more than specified max age once in update duration
See https://st.yandex-team.ru/ARMDEV-14 for usage example.
## Usage
`db_writer --config_path=<path>`
## Tool configuration
See config schema description in `proto` subdir.
## DB configuration
```sql
create table <table_name>(id serial, position geometry(POINT, 3395), t timestamp with time zone, direction float, average_speed float);
```
where
 - `position` - signal coordinates in mercator
 - `t` - signal timestamp
 - `average_speed` - signal average speed in KMPH
 - `direction` - in degrees [0..360)

Add indexes:
`CREATE INDEX signals_ts_idx ON signals USING btree (t)` - for deletion of outdated signals and filtering by time
`CREATE INDEX signals_position_idx ON signals USING gist ("position")` - for filtering by position
## Limitations
 - LogBroker reader: see `maps/wikimap/gpstiles_realtime/libs/lb_client` library client notes.
 - *Updater* performance is limited by DB: threshold signals flow is around 200K/min. It is TTK bbox for Moscow, for example.
 - Errors handling:
    - If LB client fails (throws uncatched exception), it is restarted
    - If *Updater* is not able to write signals to DB (connection fails), a warning is written to logfile, signals buffer is cleared.
 - **Note** that DB table is truncated on tool startup.