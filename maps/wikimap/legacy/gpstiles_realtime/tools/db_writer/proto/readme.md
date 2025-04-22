# db_writer configuration file schema
db_writer is configured by file in **text protobuf** format.
## Settings description
Schema `db_writer_conf.proto` consists of settings:
 - `LBConfig` - LogBroker read client configuration. See `maps/wikimap/gpstiles_realtime/libs/lb_client/proto` for more info.
 - `BBox` - region of interest in **geo** coordinates.
 - `ConnConfig` - postgres DB connection params and table to use.
 - `MaxSignalAgeMin` - max age of a signal to store. When a signal grows older, it is deleted from table.
 - `WorkerSleepDurationMin` - *Updater* and *Deleter* workers sleep duration. Signals are updated and deleted once in this time.