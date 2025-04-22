force-close
===========

Add `connection: close` to HTTP 1 responses. No effect in HTTP 2 mode. Improves L3 balancer's load distribution *under certain conditions*. Do not use if your service is a backend for an L7 balancer (which works on a per-request, not per-connection level).

Syntax
------

```yaml
- force-close
```

Options
-------

**(argument)** (default=1.0): probability of adding the header.
