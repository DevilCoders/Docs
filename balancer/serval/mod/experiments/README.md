experiments
===========

Ask UaaS to split users into boxes.

Syntax
------

```yaml
- experiments: experiments-action
```

Options
-------

**(argument)**: an action that implements the UaaS API, i.e. accepts the original request with payload removed and responds with experiment-related headers.

**trusted** (default=false): whether to use existing `x-yandex-exp*` headers in the request, if present, instead of sending a request to UaaS.

Signals
-------

**trusted_dmmm**: when `trusted` is true, the number of requests with their own values of `x-yandex-exp*`.
