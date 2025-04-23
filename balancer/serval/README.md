# serval

Kind of an HTTP load balancer.

## Usage

```sh
serval -c <config.yaml> [-l <log>]
```

## Configuration

Must be a YAML file containing a single object with the following keys:

**bind** (required): a non-empty list of primary *bind points*, i.e. URLs specifying the (interface, port) pairs to listen on and the protocol to use. Requests on connections to these points will be routed to the `main` action (see **actions** below). Examples: `http://127.0.0.1:80`, `https://[::]:443`. HTTP bind points support HTTP/1.1 and HTTP 2. Also supported are `tcp` and `tcps` bind points, which pretend a raw TCP (or TLS) connection is a `CONNECT localhost` request with no headers.

**admin** (required): a non-empty list of bind points on which the admin API is set up.

**workers** (default = # of CPUs): the number of listening threads to spawn. These threads only handle requests on the primary bind points; admin requests are handled by the initial thread. Must be at least 1.

**reuseaddr** (default = false): enable SO_REUSEADDR for listening sockets

**actions** (required): a list of single-element `name: action` maps describing the sequence of steps taken when handling the request. The `main` action is the entry point and must always be present. Example:

```yaml
actions:
- main:
  - const: "Hello, World!\n"
```

For more details and a list of supported actions, see the [module directory](/arc/trunk/arcadia/balancer/serval/mod).

**tls** (default = no TLS contexts): the OpenSSL configuration. **certs** specifies a list of certificates, **ticket-keys** is a list of paths to files containing AES128 keys for encrypting session tickets, and **ticket-ttl** is a hint for the client specifying how long a ticket will remain valid. Example:

```yaml
tls:
  certs:
  - main.pem # certificate chain and the private key in a single file
```

A single entry may contain multiple certificates with different public keys, e.g. here's one with an RSA key and one with a ECDSA key:

```yaml
  - subdomain-rsa.pem: "-" # again in a single file
    subdomain-ec.crt: subdomain-ec.key # private key stored separately from the chain
```

When the client uses SNI, the first certificate entry that is valid for the requested hostname is selected. At least one entry is required if there are any HTTPS bind points.

Among the ticket keys, the first is used to sign new sessions, while the rest are only used for decryption. The files can contain either a single key as 48 bytes of raw data, or one or more keys in "SESSION TICKET KEY" entries of a PEM file.

```yaml
  ticket-keys:
  - key-1.bin
  - key-2.pem
  ticket-ttl: 1d
```

## YAML extensions

Several things are implemented on top of the YAML format:

* `#include: X` pastes the contents of a file named `X` (relative to the current file) into this spot. If the `#include` is indented, then so is the text.

* `{{ X }}` in any line (including special directives) is replaced with the value of the environment variable `X`.

* `#default: X Y` defines a default value for the substitution of `X` if that environment variable is not defined at startup.

## Admin API

Handles paths `/X` and `/admin?action=X` for certain values of `X`.

**reload**: re-read the config file, apply the changes **except for primary bind points**; changing the set of interfaces on which connections are accepted requires a full restart. Workers are created/shut down to match the new number. Changes to actions and TLS contexts are applied to all requests and connections that happen after the reload.

**reopenlog**: if the server was started with the `-l` option, close the log file and open it for appending again. No-op otherwise.

**stat**: return the current values of all unistat signals. While signals are represented as atomic variables, collecting values of *multiple* signals is neither atomic nor ordered, so there may be discrepancies if requests are concurrently being handled.

**ping**: just a ping.

There is no graceful shutdown API; send a SIGINT or SIGTERM instead.

## Signals

Each config-defined action generates its own set of signals. See [the module directory](/arc/trunk/arcadia/balancer/serval/mod) for details.

These signals are always present, regardless of the config's contents:

**conn_dmmm**: number of client TCP connections accepted.

**conn-active_ammv**: number of client TCP connections not yet closed.

**conn-time_dhhh**: for how long each now-closed client connection existed.

**coroutines-active_ammv**: current number of coroutines in worker threads, both in run queues and waiting for events.

**coroutines-delay_avvv**: average time, in microseconds, it takes for workers to clear their run queues once.

**log-capacity_ammv**: current empty space in the log's event queue.

**log-overflow_dmmm**: number of log events dropped due to the event queue being full.

**config-reloads_dmmm**: number of times the /reload admin handle was successful.
