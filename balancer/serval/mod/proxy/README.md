proxy
=====

Forward the request into an HTTP backend or another action.

Syntax
------

```yaml
# Single backend
- proxy: action
- proxy: http://[::1]:12345

# Load balancing mode
- proxy:
  - http://[::1]:12345
  - https://[::2]:12346
  - http://127.0.0.1:12347
- proxy:
  - 2.0: action
  - 1.0: another_action

# Externally provided weights
- proxy:
  - action_a: action
  - action_b: another_action
  weights-file: controls/weights.txt
```

Options: load balancing
-----------------------

**(argument)**: a backend (action/http/https/tcp/tcps), or a list of backends or `weight: backend` maps. Default weight is 1.0. If no weights are provided, a different balancing algorithm is used that attempts to keep an equal load on each backend. **For http backends, only raw IP addresses are supported.** To resolve hostnames, gencfg groups, etc. use [the resolver tool](/arc/trunk/arcadia/balancer/serval/tools/resolver). TCP backends discard request headers, always respond with 200, and transfer the payload as raw data on a connection; TCPS is TCP over TLS.

**hash-by** (default=nothing): can be either a header name or a list of header names. If specified, the random seed for the PRNG is replaced by the hash of these headers. Requests with the same hash are always sent to the same backends, so this option also disables load-aware balancing. Header name can be tagged with `!net/mask-4/mask-6` to interpret the value as an IP address, apply a mask, and hash the result. If the request contains no values for any of the specified headers, a random seed is used as a fallback.

**weights-file**: instead of floating-point numbers, expect weights to be strings. The actual values are then frequently updated from the specified file, which must be in `name, value` format. Lines with unknown names are ignored. If the file could not be read, is missing any of the expected names, or lists all of them as zero-weight, the server will not start or reload the config; if that happens during the auto-update cycle, the old weights are retained.

**attempts** (default=number of backends): how many times to try sending the request to a backend before giving up. Must be at least 1. Each backend is only selected once per N (= the number of backends) attempts. **Note:** a particular stream may or may not be possible to read from multiple times; for example, the default HTTP/1 and H2 streams allow reading the headers multiple times, but cannot return a chunk of the payload after it has been consumed, while requests to [apphost](/arc/trunk/arcadia/balancer/serval/mod/apphost) nodes can be repeated fully as many times as desired. If re-reading a stream becomes impossible, `proxy` will terminate (and increment [a special counter](#signals)) even if there are attempts remaining.

**attempts-fast** (default=0): if non-zero, allows some failures due to ECONNREFUSED and ENETUNREACH to be retried without wasting normal attempts.

**attempt-for** (default=inf): stop retrying after this much time passes from the first attempt.

**attempt-rate** (default=inf): keep the ratio of outgoing requests to incoming requests to at most this value.

**attempt-rate-decay** (default=0.01): the ratio mentioned above is calculated as `1 / ewma(is this the first attempt?)`; this value specifies the EWMA coefficient.

**attempt-delay** (default=none): if the latest attempt does not terminate in this much time, start the next one in parallel. The attempt that writes the response headers first cancels the rest. **WARNING**:

  1. this option forces buffering of the request's entire payload;
  2. it only works properly if all backend actions send responses (and not, say, modify the request headers and then return);
  3. if no response is finished in *attempt-for* (see above), all attempts are cancelled by timeout;
  4. if the value is too low (less than 1-2 RTT), some fast attempts may be counted as normal ones instead.

**else** (default=nothing): the action to run when out of attempts. If not specified, the error is propagated upwards. (If the error reaches the root of the `main` action, the connection to the client will be closed without sending a response.)

Options: remote connections
---------------------------

These options only affect http/https backends in the same `proxy` call. They have no effect on action backends, including nested `proxy`.

**conn-timeout** (default=25ms): how long to wait for `connect()` to succeed.

**recv-timeout** (default=inf if both attempt-for and attempt-delay are specified, else 5s): fail an attempt if a single read operation takes too long to complete. The read operations are: 1. receiving a *single complete* header list (of which responses can have several, all but the last with a 1xx code); 2. fetching *a chunk* (can be as small as 1 byte) of the response payload; 3. obtaining *all* trailers. **Note:** even if sync mode (see below) is disabled, this timeout is not started until the upload is complete. To limit the time spent doing *that*, use this:

**send-timeout** (default=recv-timeout): fail an attempt if a single *write* operation is too slow. Write operations are exactly the inverse of read operations: transmit all headers, send at least a byte of the payload, and submit the trailers (though requests normally don't have those).

**keepalive** (default=30s): for how long to keep unused connections online. This timeout is not guaranteed to be precise, i.e. connections may be closed a bit later. If multiple calls to `proxy` have backends in common, the keepalive pools for these backends are shared, and it's not particularly defined which keepalive timeout will be used.

**retry-codes** (default=none): which response codes should be converted into network errors (and therefore retried if there are attempts remaining). The argument should be either a single code-spec, a list of code-specs, or a map of code-specs to either "normal" or "fast" (see `attempts` vs `attempts-fast` above). Code-spec is either a number or a code class (e.g. 5xx). For example, `retry_codes: {503: fast, 5xx: normal}` results in 503 responses being equivalent to ECONNREFUSED, and other 5xx responses to ECONNRESET.

**sync** (default=false): assume that backends will not respond before completely reading the request's payload, if it exists. This allows saving some memory and CPU cycles since writing and reading can be done sequentially rather than in parallel.

Signals
-------

**requests_dmmm**: the total number of outbound requests.

**errors_dmmm**: the number of outbound requests that have failed for one reason or another.

**errors-\*_dmmm**: versions of the above signal that count some known errors.

**failures_dmmm**: the number of inbound requests that have failed because of a backend error.

**failures-unreplayable_dmmm**: the number of inbound requests that have failed because of a backend error that occurred after a point of no return: either a part of the response has already been sent, or a part of the request's payload has been read and was not stored in any buffer.

**time_dhhh**: outbound requests, split into buckets depending on the time it took for the backend to finish.

**conn-time_dhhh**: for http/https backends, the time it took to connect.

**overload_avvv**: the current ratio of outbound requests to inbound ones; see the `attempt-rate` option. To view this signal in golovan, it needs to be wrapped in `aver(...)`, e.g. `signals=aver(main-upstream-overload_avvv)`.
