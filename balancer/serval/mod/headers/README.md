{request,response}-headers
==========================

Add or remove HTTP headers.

Syntax
------

```yaml
- request-headers:
  - !erase x-by-regexp-.*
  - !erase x-literal
  - x-add-unconditionally: value
  - x-forwarded-for: !ip .
  - !weak x-add-if-not-exists: value
  - x-forwarded-for-copy: !header x-forwarded-for
  - x-cookie-abc: !cookie abc
```

**Note:** the most recent (i.e. last in config order) `response-headers` will execute its actions first. Essentially, `response-headers` adds a hook to a stack; the stack is emptied, and hooks are evaluated, when responding. Headers are not added to 1xx responses, except 101.

**Really note**: all header names should be in lowercase, because HTTP 2.

Options
-------

**(argument)**: the list of operations to do on the headers. Each operation is either `!erase regexp` or an addition of a new header. Additions tagged as `!weak` are only performed if the specified header does not yet exist. Adding a header does not remove the old values.

Functions
---------

The value may be tagged with a function name, in which case it is interpreted as an argument to that function and used to construct the real string value. Currently supported:

**!ip**: format the *real* IPv4/6 address of the client. IPv6 is printed without enclosing brackets, and the port is omitted. The argument is ignored.

**!port**: the port of the IPv4/6 client. The argument is ignored.

**!time**: print current time in microseconds since 1970-01-01 00:00:00 UTC. The argument is ignored.

**!header**: copy the value of an existing header. The argument is the source header's name.

**!cookie**: copy the value of the argument cookie. The argument is the source cookie's name. 
