resolver
========

Construct backend lists for use by the [proxy](/arc/trunk/arcadia/balancer/serval/mod/proxy) action.

Usage
-----

First run:

```sh
./resolver < spec.yaml > backends.yaml
```

Then do something like this in the config:

```yaml
#include: backends.yaml

actions:
- main:
  - proxy: *GROUP_NAME
```

Subsequent runs:

```sh
diff -U 0 -F '  .*: &.*' backends.yaml <(./resolver --update backends.yaml < spec.yaml | tee new-backends.yaml)
```

See [example.yaml](/arc/trunk/arcadia/balancer/serval/tools/resolver/example.yaml) for an example of the input.
