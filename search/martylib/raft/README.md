### Raft

https://raft.github.io/

---

This library helps to synchronize state of python objects between instances of one Nanny service
using `PySyncObj`, which built on raft consensus algorithm.

You can synchronize state of objects, which base is `SyncObjConsumer` (https://github.com/bakwc/PySyncObj)

Usage:
```python
from search.martylib.raft import Raft, MasterLock


def main():
    ...
    lock = MasterLock()
    Raft.prepare('nanny-service-id', port=8956)
    ...
```

Then you can run your application with arguments `./your_app run raft ...`
and use raft objects in your code. For example
```python
with lock:
    do_something_with_master_lock()
```

Metrics:
`unistat-global-raft-node-status-<instance_fqdn>`
 - FOLLOWER: 0
 - CANDIDATE: 1
 - LEADER: 2 