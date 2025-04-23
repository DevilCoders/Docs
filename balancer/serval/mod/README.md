Built-ins
=========

Various predefined actions. See README files for the specifics of each one.

Actions and action calls
------------------------

An action is simply a function that takes a stream (in HTTP 2 sense, i.e. a request-response pair) and does something with it: modifies the request headers, reads the payload, writes a response, etc. There are two kinds of actions: built-ins, defined in C++ code, and config-defined ones.

Because the config file is not a program, all a config-defined action can do is call some other actions. This is what config-defined actions look like:

```yaml
actions:
# An action call is a string containing the name of the action:
- main: do-something
# Or a map with arguments, where the first key specifies the action:
- do-something: {do-something-else: "with an argument", and: another-argument}
```

Actions can be called in a sequence, which is evaluated top to bottom until a complete response is constructed. As soon as an action closes the stream or fails, the sequence is cancelled. Anywhere an action call is expected, a sequence can also be used.

```yaml
actions:
- main:
  - do-something-but-dont-write-a-response
  - write-a-response
```

If a call to the `main` action does not result in a response, the connection will be closed.

Signals
-------

For each config-defined action, the following unistat signals are generated, prefixed with the action name and a dash.

**requests_dmmm**: the total number of calls to this action.

**requests-active_ammv**: the number of calls to this action that have not yet finished at the time of stat collection.

**failures_dmmm**: the number of times evaluation of the action terminated with an error.

**cancelled_dmmm**: the number of requests aborted by the client.

**time_dhhh**: a histogram containing the number of calls to the action grouped into buckets depending on the time it took for the call to terminate.

In addition, actions, both built-in and config-defined, may produce per-call statistics. By default, these signals are ignored. To collect them, the call must be tagged with a stat ID:

```yaml
- !call-to-do-something do-something
```

An action call tagged `!T` in a config-defined action `C` would produce signals that begin with `C-T-`, or just `C-` if `T` is an empty string. If an action call is specified as an argument to another action call and both have stat IDs, they are joined with a dash when constructing the prefix for the inner call:

```yaml
actions:
- main:
  # main-outer-<signal name>:
  - !outer call-this:
    # main-outer-inner-<signal name>:
    - !inner nested-action-call
    # main-outer-<signal name>:
    - ! another-one
    # signals are discarded:
    - and-another
```

If there's a name collision, the signals are aggregated. For example, if two calls that use `requests_dmmm` are tagged in such a way that the signals have identical prefixes, there will only be one signal that contains the sum of two values.

Sequences and calls to config-defined actions, when tagged, produce the signals described above, except this time they count only the requests that have triggered the tagged call.
