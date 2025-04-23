static
======

Serve files from a local directory.

Syntax
------

```yaml
- static: /var/www/root/
```

Options
-------

**(argument)**: the directory to serve files from, either absolute or relative to cwd.

**if-not-found** (default=a very simple 404 page): what to respond with if the file does not exist, is not readable, or is a directory.

**if-not-get** (default=a very simple 405 page): what to respond with if the method is neither GET nor HEAD.
