h100
====

If the client wants 100 Continue before it starts transferring the payload, send that response on first attempt to read the data. (Note: `proxy` supports forwarding 1xx responses, so unless [some other action](/arc/trunk/arcadia/balancer/serval/mod/antirobot) wants a piece of the payload or the backend does not support `expect: 100-continue`, this action is unnecessary.)

Syntax
------

```yaml
- h100
```

Options
-------

None.
