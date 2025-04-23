## Yandex.IO libraries

### Rationale
`libs/` is intended for "general-purpose" libraries:
* not device-specific
* without nasty side effects like implicitly reading values from configuration
* each library should serve a single well-defined purpose

### Contents
* `audio_player`: Audio player/mixer interface and implementation
* `errno`: A C++ exception wrapper for C `errno`
* `error_correcting_code`: Reed-Solomon encoding for `sound_initd` audial tokens
* `http_client`: Curl-based HTTP client
* `ipc`: High-level Quasar IPC implementation for client-server communication
* `jwt`: JWT tokens support for glagol authentication
* `logging`: Debug logging interface
* `ping`: ICMP ping implementation
* `sqlite`: Sqlite database wrapper for appmetrica
* `telemetry`: Interface for sending telemetry events
* `threading`: Custom thread-based concurrency primitives
* `websocket`: WebSocket client/server support (`websocketpp` wrappers)
