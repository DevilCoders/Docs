# Combctl

## Commands

### graph_prepare

#### local run
Build
* ensure `CGO_ENABLED` build flag is set to `1` (build via `ya make` sets it correctly)

Run
* set environment variable YT_TOKEN
* place tvm token to `/arcadia/market/combinator/auth_token` file. This may be done by running `/arcadia/market/combinator/run_tvmtool script`
* run `combctl graph-prepare`
  * use `--mr` option if you need to do actual map reduce. Without this flag set graph validation fails.
  * use `--force` option to force recalculate graph.
