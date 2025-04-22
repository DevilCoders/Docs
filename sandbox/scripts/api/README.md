# Interactive shell for Sandbox API

The fast way to get a Python shell with an already authenticated Sandbox client:

```bash
arcadia$ ya py sandbox/scripts/api
```

The script creates a global variable `api` with the client object:

```bash
arcadia$ ya py sandbox/scripts/api
Creating temporary PY3_PROGRAM /home/mkznts/arcadia/junk/mkznts/_ya_py
Baking shell with:
 sandbox/scripts/api (program)
Ok
Authenticated as mkznts
Python 3.7.4 (default, Oct 16 2019, 15:46:28)
Type 'copyright', 'credits' or 'license' for more information
IPython 7.8.0 -- An enhanced Interactive Python. Type '?' for help.

In [1]: api.user.current.read()["login"]
Out[1]: 'mkznts'

In [2]: api.task(type='TEST_TASK_2', owner='mkznts')["id"]
Out[2]: 529214086

In [3]: api.batch.tasks.start.update({"id": 529214086})
Out[3]:
[{'status': 'SUCCESS',
  'message': 'Task started successfully.',
  'id': 529214086}]
```

Automatic authentication requires your private ssh key from Staff loaded into `ssh-agent`.
