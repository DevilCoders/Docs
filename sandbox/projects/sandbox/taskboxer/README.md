**TASKBOXER_TASK** is special task that should be executed as binary task.
Task has two implementations:
1) The one that is importable in tasks archive.
It has only task class declaration to ensure that server know the task type.
2) The one that is impossible to import in tasks archive.
This implementation declares task parameters, requirements and does all the stuff.

To ensure unreachability of second implementation there is no `isolated/__init__.py` file.
Also there is no `PEERDIR` to `isolated/bin`.