match
=====

Conditionally execute actions depending on whether a header matches a regexp.

Syntax
------

```yaml
# Regexp mode:
- match: user-agent
  !i ".* Chrome/.*": chrome
  ".* AppleWebKit/.*":
  - safari

# Source mode:
- match: :source
  127.0.0.0/255.0.0.0: lo4
  ::1/128: lo6

# Method mode:
- match: :method
  GET: on_get
  POST: on_post

# Path mode:
- match: :path
  /abc: on_abc
  /123: on_123
```

Options
-------

**(argument)**: the name of the header to match. Can also be the `:path`, `:method`, and `:authority` HTTP 2 pseudo-headers, which work in HTTP 1 mode as well. (By contrast, `host` does not work even in HTTP 1 mode; it must *always* be specified as `:authority`.)

**(everything else)**: the regular expression to match against, and the action to execute if it matches. If the header has multiple values, matching any one of them is enough. If a header matches multiple regexps, the actions are executed top to bottom, stopping at the first one that sends a complete response, if any. If no regexp matches (or the header has no values), nothing is executed, and the request simply falls through to the next action unmodified.

If the argument is `:source`, instead of matching a header by regexps, the client's IP address is checked for being located within one of the networks listed. Cases should be either `network/mask`, or arbitrarily nested lists of such. IPv6 addresses can be in square brackets, and mask is either a complete bit pattern (e.g. `255.255.8.0` for IPv4, `ffff:ff0f::` for IPv6) or a suffix (0-32 for IPv4, 0-128 for IPv6).

Cases can be tagged with flags, e.g. `!i` or `!in`. Supported flags:

**i**: case-insensitive match.

**g**: match any substring — equivalent to wrapping the expression in `.*`.

**p**: match a path prefix — equivalent to appending `(/.*)?`.

**n**: negate a match — run the action if the regexp does *not* match. Only this flag is supported when matching the address.
