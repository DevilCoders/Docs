python-conductor-client
=======================

python-conductor-client provides python interface to Conductor v1 API, which
uses OAuth authorization to view and edit data in Conductor.

Installation
------------

python-conductor-client could be installed by pip:

```
pip install git+git://github.yandex-team.ru/devtools/python-conductor-client.git
```

Configuring
-----------

Conductor v1 API requires OAuth token for access. It could be generated there:

https://oauth.yandex-team.ru/authorize?response_type=token&client_id=eb3c509c74b649cd8411ffc154543fe0

(click "Confirm" and you will see your OAuth token in the ```token``` parameter of
URL where you will be redirected)

Put it in ```~/.conductor_client.ini``` file:

```ini
[conductor_client]
path = http://c.yandex-team.ru/api/v1
token = 649cd8...
```

**Do not forget to ```chmod 600 ~/.conductor_client.ini```!**

You also can specify token by using ```conductor_client.set_token``` function.
And custom Conductor API URL could be set by ```conductor_client.set_path```
function.

Usage
-----

To use client you need to import model classes:
```python
from conductor_client import *
```

Getting group:
```python
group = Group(name='conductor')
print "Group #%s has %s hosts" % (group.id, len(group.hosts))
```

Handling 404 exceptions:
```python
group = Group(name='i_do_not_exist')
try:
    print group.id
except Group.NotFound:
    pass
# OR
if group.exists():
    pass
```

Creating group:
```python
group = Group(name='my_new_group')
group.project = Project(name='conductor')
group.description = 'For this and that'
success = group.save()
if not success:
    print group.errors()
```

Updating group:
```python
group = Group(name='conductor')
group.description = 'This description is better'
group.save()
```

Some semi-useful snippet:
```python
project = Project(name='conductor')
groups_without_parents = filter(lambda g: len(g.parent_groups) == 0, project.groups)
if len(groups_without_parents) > 1:
    whole_project_group = Group(name=project.name + '-all', project=project)
    whole_project_group.description = "All groups in %s project" % project.name
    if not whole_project_group.exists():
        whole_project_group.save():
        for group in groups_without_parents:
            group.parent_groups.append(whole_project_group)
```
