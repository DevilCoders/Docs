# Deprecated method

You should use juggler-sdk instead ansible-juggler.

## Why?

Ansible-juggler doesn't support python3 (contains reserved keyword `async` and etc)  
and we've troubles on Ubuntu Focal systems with it.

## How to use juggler-sdk?

```
$ jsonnet <config> | juggler-sdk load --force
```

You may check difference between current version and the next with --dry-run option:

```
$ jsonnet <config> | juggler-sdk load --force --dry-run
```

Enjoy jsonnet and juggler-sdk.
