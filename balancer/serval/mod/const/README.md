const
=====

Send a hardcoded response or a static file.

Syntax
------

```yaml
- const: "Forbidden\n"
  :code: 403
  x-go-somewhere-else: "1"
```

Options
-------

**(argument)**: the payload. Must be empty for codes 204 and 304. If tagged with `!file`, this should be a path to a file that is read at config load.

**:code** (default=200): the HTTP status code.

**:tail** (default=none): HTTP trailers, in the same format as the headers (see below).

**(everything else)**: HTTP headers. Names must be lowercase, values must be strings or lists of strings. A list of values is equivalent to specifying the header once with each value separately. Name cannot be `content-length`, which is added automatically.
