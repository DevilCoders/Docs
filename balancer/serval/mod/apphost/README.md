apphost
=======

Evaluate an [AppHost](https://wiki.yandex-team.ru/apphost/) graph.

Syntax
------

```yaml
- apphost:
  - RESPONSE:
    - NODE1
    - NODE2: "NODE3[flag1] && (!NODE4[flag2] || NODE5[flag3])"
  - NODE1:
    - !json_item_type {some_keys: [with_values]}
  - NODE2:
    - NODE3
    proxy: http://[::1]:12345
```

Options
-------

**(argument)**: the graph, as a list of nodes.

Some nodes are simple strings; these specify what should be expected as the input of this graph.

```yaml
- REQUEST
```

Others take lists of inputs and produce a single output each: those define transformations of the input, where the output of the RESPONSE node defines the output of the entire graph. By default, nodes are *transparent*, meaning their output is simply the concatenation of all inputs.

```yaml
- RESPONSE: # duplicate each input:
  - REQUEST
  - REQUEST
```

Instead of a node name, an input can be a constant map tagged with an apphost item type, in which case it is encoded as JSON. (Unquoted strings are interpreted as booleans and numbers when possible.)

```yaml
- RESPONSE:
  - !something {value: "this is a constant response", really: true}
```

For more complex transformations, a node can have an arbitrary action attached to it. The action should accept a protobuf-encoded service request (`NAppHostProtocol.TServiceRequest` or wire-compatible) as payload and produce a protobuf-encoded response (`NAppHostProtocol.TServiceResponse`).

```yaml
- RESPONSE: # forward the input through a network service:
  - REQUEST
  proxy: http://[::1]:12345
  conn-timeout: 5ms
  recv-timeout: 1s
```

The `apphost` action itself also satisfies this interface. In this case, the names of the inputs should match the ones that the graph expects.

```yaml
actions:
- graph-x:
  - apphost:
    - REQUEST
    - NODE1: [REQUEST]
    - RESPONSE: [NODE1, REQUEST->NODE2]
      graph-y: .
- graph-y:
  - apphost:
    - NODE1
    - NODE2
    - RESPONSE: [NODE1, NODE2]
      proxy: http://[::1]:12345
```

By default, the request is sent to path `/`. If the action has an argument named `path`, its value is used instead. If it has the `grpc` argument set to `true`, an emulation of the gRPC protocol is used to call the method `Invoke` on an `NAppHostProtocol.TServant`. Together with [proxy](/arc/trunk/arcadia/balancer/serval/mod/proxy)'s HTTP 2 mode, this allows sending requests to real gRPC-based backends.

Each input/output consists of a sequence of JSON or Protobuf *items* tagged with *types*, plus a set of string *flags*. When a node is specified as an input, all items and flags from its output are taken. If only items of certain types are desired, they can be listed like so:

```yaml
- RESPONSE:
  - REQUEST@something,something_else
```

This also removes all flags from the input. Additionally, if the type should be changed, the new type can be specified after an arrow:

```yaml
- RESPONSE:
  - REQUEST@something->a,something_else->b
```

Prefix each type with a minus sign to transfer everything *except* items of the listed types:

```yaml
- RESPONSE:
  - REQUEST@-redundant,-useless
```

Since generally only a single item, the first of the last, of each type is needed, there is a built-in way to select them:

```yaml
- RESPONSE:
  - ^REQUEST # first item of each type
  - $REQUEST # last item of each type
```

Edges can be conditional on whether the output of nodes contains items of specified types or flags with specified names.

```yaml
- RESPONSE:
  - REQUEST: "REQUEST[should_forward]"
```

These conditions can use the `&&`, `||`, `? :`, and `!` operators, as well as parentheses, with usual (C) semantics and precedence rules. A special flag named `noans` is set for a node if its associated action failed to produce a response.

If, right before executing a node's action, all paths from that node to RESPONSE have an edge with a condition that evaluates to "false" in [ternary logic](https://en.wikipedia.org/wiki/Three-valued_logic#Kleene_and_Priest_logics), or the node is explicitly disabled via `srcskip`, its action is not actually executed, and `noans` is set. If an action has already started, but edge expression evaluation concurrently removes `RESPONSE`'s dependence on it, the action is cancelled when graph evaluation is finished.

If a node's output is not used for `RESPONSE`, it can be marked as *async*. The `async` option's value is the condition under which the node should be visited, or `true` if it is unconditional.

```yaml
- RESPONSE:
  - REQUEST
  proxy: http://[::1]:12345
- CACHE_STORE:
  - REQUEST
  - RESPONSE
  proxy: http://[::1]:31337
  async: "!RESPONSE[noans]"
```

For purposes of skipping unused actions, async nodes are treated the same way as RESPONSE so long as their condition's value is true or unknown.

Edge expressions (and async conditions) do not create dependencies: if an expression in node A uses a flag of node B, but A does not otherwise (transitively) depend on B, that expression may be evaluated before B actually completes. In that case, it appears as if it had failed, i.e. `noans` is set, and everything else isn't.

Nodes can also be marked as `streaming: true`; in that case, a connection is opened as soon as at least one input is ready, and other inputs are transmitted as (and in the order) they become available. Currently, this is useful for nested `apphost` actions, gRPC backends, and transparent `RESPONSE` (see [http-to-apphost](#http-to-apphost) below); everything else, including non-`RESPONSE` transparent nodes, will simply buffer all inputs before producing an output. If you need to enforce a particular ordering of inputs, use additional transparent nodes.

A fair warning
--------------

The process described above is in some ways different from how the real apphost does it.

* Over an `A->B` edge, apphost will always transmit A's flags as long as at least one item is transferred on that same edge. Type filters only affect that insofar they change the number of items. This action behaves as if flags were in an item of their own, with a type that you can't explicitly state.

* Given a straightforward linear graph `A->B->C` with a condition on `B->C` that at the time of visiting A references at least one node that has not finished yet, apphost will visit A, *even if other nodes' flags already force the expression to always become false regardless*. This action will do its best to short-circuit the expression, and avoid visiting A if its SAT-solving code succeeds in proving that there are no truthy assignments of unknown flags.

Signals
-------

Actions attached to nodes are automatically assigned stat ids equal to the nodes' names; for example,

```yaml
- A: [...]
  proxy: ...
```

will produce **A-errors_dmmm**, etc. In addition, the following signals are generated for each node:

**NAME-visits_dmmm**: the number of times this node's action was evaluated.

**NAME-crit-path_dmmm**: the number of visits which happened to be on the critical path from any input node to RESPONSE.

**NAME-req-size_dhhh**: a histogram of request sizes. For nodes with `streaming: true`, this counts separate chunks.

**NAME-rsp_size_dhhh**: a histogram of response sizes.

---

apphost-hasher
==============

Generate balancing hints for apphost graph nodes. These hints can be used by setting the `hash-by` option of `proxy` actions attached to nodes to the `x-apphost-hint` header.

Syntax
------

```yaml
apphost-hasher:
  NODE1: [[type, field, 0, another_field]]
```

This action implements the apphost protocol.

Options
-------

**(argument)**: the map of node names to sequences of JSON paths. The first element of each path is the type of an apphost item (the last value of that type is used), while the rest are array indices or object fields. Duplicate paths are discarded, and the order does not matter.

---

apphost-to-http
===============

Given a protobuf apphost item of type `http_request` (`NAppHostHttp::THttpRequest`), construct an arbitrary request to another service, then convert the response into a protobuf item of type `http_response` (`NAppHostHttp::THttpResponse`).

Syntax
------

```yaml
apphost-to-http: http://example.com
```

This action implements the apphost protocol.

Options
-------

Same as [proxy](/arc/trunk/arcadia/balancer/serval/mod/proxy).

---

http-to-apphost
===============

Convert an arbitrary HTTP request into an apphost item, and use data from resulting items to construct a response. More specifically, the request is encoded as an item of node `HTTP_REQUEST` with type `http_request` containing a JSON object that looks sort of like this:

```json
{
    "type": "http_request",
    "remote_ip": "2a02:6b8:a::a",
    "request_time": "1550237161",
    "method": "GET",
    "uri": "/search/?text=test&lr=213",
    "headers": [["user-agent", "fake-request/0.1"]],
    "content": ""
}
```

And the response is expected to consist of `http_response` items that look like this:

```json
{
    "status_code": 200,
    "headers": [["set-cookie", "yandexuid=1234567890"]],
    "content": "<!doctype html>..."
}
```

The response may contain many such items in multiple chunks (each corresponding to a `streaming` transparent `RESPONSE`'s input, if it is actually one; see [apphost](#apphost) above) containing such items. `status_code` is only taken from the first item, while `headers` are merged from the entire first chunk. If `status_code` is not set, it defaults to 200 if there is at least one item, else 204.

Syntax
------

```yaml
- http-to-apphost
- apphost:
  - HTTP_REQUEST
  - RESPONSE: [...]
```

Options
-------

None.
