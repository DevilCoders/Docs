# Sandbox API Client

`sandbox/common/rest` is a py23-compatible Sandbox API client.

## Installation

### For Arcadia Projects

Add `sandbox/common/rest` into PEERDIR of your `ya.make` file.
The client module can be imported via `from sandbox.common import rest`

### Outside Arcadia

The client is also available as part of [sandbox-library](https://pypi.yandex-team.ru/dashboard/repositories/default/packages/sandbox-library/) package in the internal PyPI:
```bash
pip install -i https://pypi.yandex-team.ru/repo/default sandbox-library
```

The import path is the same: `from sandbox.common import rest`

### Sandbox Tasks

There is an already initialised API client in Sandbox tasks that can be used via:
* task object attribute `self.server`
* global thread-local object: `sdk2.Task.server`

You can also create it manually with `rest.Client()`. In all cases the client will be automatically authenticated with the task author.


### Interactive Shell

If you use Arcadia via [arc](https://wiki.yandex-team.ru/arcadia/arc/) (or SVN with `arcadia/sandbox` checked out) there is a fast way to get a Python shell with an already authenticated Sandbox client:

```bash
# Python 2:
arcadia$ ya py sandbox/scripts/api  # sandbox/scripts/api/py2 works as well

# Python 3:
arcadia$ ya py sandbox/scripts/api/py3
```

The script creates a global variable `api` with the client object:

```bash
arcadia$ ya py sandbox/scripts/api/py3
Creating temporary PY3_PROGRAM /home/mkznts/arcadia/junk/mkznts/_ya_py
Baking shell with:
 sandbox/scripts/api/py3 (program)
Ok
Authenticated as mkznts
Python 3.7.4 (default, Oct 16 2019, 15:46:28)
Type 'copyright', 'credits' or 'license' for more information
IPython 7.8.0 -- An enhanced Interactive Python. Type '?' for help.

In [1]: api
Out[1]: <sandbox.common.rest.Client at 0x7f157c3dfd50>
```

Automatic authentication requires your private ssh key from Staff loaded into `ssh-agent`.