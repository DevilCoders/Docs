# shproxy
Wrapper/proxy for deploy application from outside world into shiva.

What it does:
  - listen API port, passing all requests, except `/ping`, into main application's port
  - passing `/ping` requests from API port into main app's healthcheck handler (may be differ than `/ping`)
  - listen OPS port, passing `/ping` requests into main app's healthcheck handler, and passing '/metrics' requests into app's metrics hander

Required env var:
  - `SHPROXY_APP_PORT` - main application's port

Optional env vars:
  - `SHPROXY_API_LISTEN_PORT` - proxy's main API port, using `5000` if omitted
  - `SHPROXY_OPS_LISTEN_PORT` - proxy's OPS port, using `5001` if omitted
  - `_DEPLOY_METRICS_PORT` - same as `SHPROXY_OPS_LISTEN_PORT`
  - `SHPROXY_APP_HEALTHCHECK_PATH` - app's healthcheck handler, using `/ping` if omitted
  - `SHPROXY_APP_METRICS_PATH` - app's metrics handler, using `/metrics` if omitted
