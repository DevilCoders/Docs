antirobot
=========

Stop those who can't harm humans from harming servers by redirecting them to a CAPTCHA.

Syntax
------

```yaml
- h100
- antirobot: antirobot-action
```

Options
-------

**(argument)**: an action that implements the antirobot API, i.e. accepts a `POST /fullreq` with payload containing an HTTP/1.1-encoded request, and responds with either a redirect with `x-forwardtouser-y` set to 1, or 200 OK with `x-yandex-internal-request` and `x-yandex-suspected-robot` set to 0 or 1.

**cut-payload** (default=512): the number of bytes from the payload to also send to antirobot. Any value other than 0, including the default, requires a [h100](/arc/trunk/arcadia/balancer/serval/mod/h100) action to automatically send 100 Continue.

Signals
-------

**captchas_dmmm**: the number of times antirobot's response has been forwarded to the client.
