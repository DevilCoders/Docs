# Getting Started

### Installation

This Python package provides a `setup.py` file, so you can install it in any way you prefer.

### Running tests

You can run tests using `tox`. See `tox.ini` for details.

### Creating workflows

Here is a `demo.py` script that executes some demo tasks:

```python
"""
A comprehensive example of a workflow.

Just generates some text file, enumerates its lines, and removes the original file.

Runs the workflow repeatedly every 5 seconds in 2 processes.
In order to stop the workflow, hit Ctrl+C.
You should find the result in the `output` file.

Let it run a couple of times and examine the log.
"""

import logging
import os
import os.path

from edera import Condition
from edera import Parameter
from edera import Parameterizable
from edera import Task
from edera.daemon import Daemon
from edera.daemon import DaemonWorkflowDescriptor
from edera.daemon import RunDaemonWorkflow
from edera.lockers import DirectoryLocker
from edera.qualifiers import Integer


class PathExists(Condition, Parameterizable):

    path = Parameter()

    def check(self):
        return os.path.exists(self.path)


class GenerateFileWithSomeData(Task, Parameterizable):

    path = Parameter()

    def execute(self):
        with open(self.path, "w") as stream:
            stream.write("some\ndata\n")

    @property
    def target(self):
        return PathExists(path=self.path)


class EnumerateLinesInFile(Task, Parameterizable):

    input_path = Parameter()
    output_path = Parameter()
    start = Parameter(Integer, default=1)

    def execute(self):
        with open(self.input_path, "r") as input_stream:
            with open(self.output_path, "w") as output_stream:
                for index, line in enumerate(input_stream, self.start):
                    output_stream.write("%d\t%s" % (index, line))

    @property
    def target(self):
        return PathExists(path=self.output_path)


class RemoveFile(Task, Parameterizable):

    path = Parameter()

    def execute(self):
        try:
            os.remove(self.path)
        except OSError:
            pass

    @property
    def target(self):
        return ~PathExists(path=self.path)


class GetOutput(Task, Parameterizable):

    @property
    def requisite(self):
        generate_file = GenerateFileWithSomeData(path="input")
        process_file = EnumerateLinesInFile(input_path=generate_file.path, output_path="output")
        remove_file = RemoveFile(path=generate_file.path)
        return {
            self: process_file,
            process_file: generate_file,
            remove_file: process_file,
        }


class RunMyWorkflow(RunDaemonWorkflow):

    @property
    def _locker(self):
        return DirectoryLocker("locks")


def run():
    # configure logging
    handler = logging.StreamHandler()
    handler.setFormatter(logging.Formatter("%(asctime)s - %(processName)s/%(threadName)s - %(name)s - %(levelname)s - %(message)s"))
    logging.getLogger().addHandler(handler)
    logging.getLogger().setLevel(logging.WARN)
    logging.getLogger("edera").setLevel(logging.INFO)
    # try to get the output
    runner = RunMyWorkflow(task=GetOutput())
    descriptor = DaemonWorkflowDescriptor(runner=runner, degree=2, delay="PT5S")
    # prepare a directory for locks
    if not os.path.exists("locks"):
        os.mkdir("locks")
    Daemon([descriptor]).run()


if __name__ == "__main__":
    run()
    # check `output` and see "1\tsome\n2\tdata\n"
```

Let's run it!

```bash
$ python demo.py  # then after about 8 seconds hit Ctrl+C
```

```
.. - MainProcess/MainThread - .. - INFO - Starting daemon
.. - -/- - .. - INFO - Starting slaves
.. - Online/- - .. - INFO - Running task SustainDaemonWorkflows(descriptors=[DaemonWorkflowDescriptor(degree=2, delay=PT5.000000S, interruption_timeout=PT60.000000S, label='GetOutput', runner=RunMyWorkflow(task=GetOutput()))])
.. - Online/- - .. - INFO - Starting slaves
.. - GetOutput/- - .. - INFO - Starting slaves
.. - GetOutput#2/- - .. - INFO - Starting slaves
.. - GetOutput#1/- - .. - INFO - Starting slaves
.. - GetOutput#1+/- - .. - INFO - Trying to normalize the workflow
.. - GetOutput#2+/- - .. - INFO - Trying to normalize the workflow
.. - GetOutput#1+/- - .. - INFO - Trimming the workflow
.. - GetOutput#1+/- - .. - INFO - Workflow trimmed: 2 out of 4 tasks left
.. - GetOutput#1+/- - .. - INFO - Running task RemoveFile(path='input')
.. - GetOutput#1+/- - .. - INFO - Pre-checking (~PathExists(path='input') & PathExists(path='output'))
.. - GetOutput#1+/- - .. - INFO - Task RemoveFile(path='input') already completed (ignored)
.. - GetOutput#1+/- - .. - INFO - Task RemoveFile(path='input') completed
.. - GetOutput#2+/- - .. - INFO - Trimming the workflow
.. - GetOutput#2+/- - .. - INFO - Workflow trimmed: 2 out of 4 tasks left
.. - GetOutput#2+/- - .. - INFO - Running task RemoveFile(path='input')
.. - GetOutput#2+/- - .. - INFO - Pre-checking (~PathExists(path='input') & PathExists(path='output'))
.. - GetOutput#2+/- - .. - INFO - Task RemoveFile(path='input') already completed (ignored)
.. - GetOutput#2+/- - .. - INFO - Task RemoveFile(path='input') completed
.. - GetOutput#1/- - .. - INFO - Starting slaves
.. - GetOutput#2/- - .. - INFO - Starting slaves
.. - GetOutput#2+/- - .. - INFO - Trying to normalize the workflow
.. - GetOutput#1+/- - .. - INFO - Trying to normalize the workflow
.. - GetOutput#1+/- - .. - INFO - Trimming the workflow
.. - GetOutput#2+/- - .. - INFO - Trimming the workflow
.. - GetOutput#1+/- - .. - INFO - Workflow trimmed: 2 out of 4 tasks left
.. - GetOutput#1+/- - .. - INFO - Running task RemoveFile(path='input')
.. - GetOutput#2+/- - .. - INFO - Workflow trimmed: 2 out of 4 tasks left
.. - GetOutput#1+/- - .. - INFO - Pre-checking (~PathExists(path='input') & PathExists(path='output'))
.. - GetOutput#2+/- - .. - INFO - Running task RemoveFile(path='input')
.. - GetOutput#1+/- - .. - INFO - Task RemoveFile(path='input') already completed (ignored)
.. - GetOutput#1+/- - .. - INFO - Task RemoveFile(path='input') completed
.. - GetOutput#2+/- - .. - INFO - Pre-checking (~PathExists(path='input') & PathExists(path='output'))
.. - GetOutput#2+/- - .. - INFO - Task RemoveFile(path='input') already completed (ignored)
.. - GetOutput#2+/- - .. - INFO - Task RemoveFile(path='input') completed
.. - -/- - .. - WARNING - Interrupted: SIGINT/SIGTERM received
.. - Online/- - .. - WARNING - Interrupted: SIGINT/SIGTERM received
.. - GetOutput#2/- - .. - WARNING - Interrupted: SIGINT/SIGTERM received
.. - GetOutput#1/- - .. - WARNING - Interrupted: SIGINT/SIGTERM received
.. - GetOutput#1/- - .. - WARNING - Interrupted: SIGINT/SIGTERM received
.. - GetOutput#2/- - .. - WARNING - Interrupted: SIGINT/SIGTERM received
.. - Online/- - .. - WARNING - Interrupted: SIGINT/SIGTERM received
.. - -/- - .. - INFO - Daemon stopped
```

Enjoy!

### Logging

We highly recommend you to use [`logging.handlers.SysLogHandler`](https://docs.python.org/2/library/logging.handlers.html#sysloghandler)
in combination with a syslog-compatible service like [`syslog-ng`](https://syslog-ng.org)
to implement logging in your application.
It seems to be the only reliable way to organize multi-process logging effortlessly.
