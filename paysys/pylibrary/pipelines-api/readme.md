# Pipeline API

pipelines_api - library for launch pipelines in timeline.

Usage - see example.py:
```python
from pipeline_api import buildLaunchCommand, PipelineLauncher
from pipeline_api.pipes import oebs
from pipeline_api.pipes.resources.event import Event

launcher = PipelineLauncher(endpoint='http://localhost:8042')

res = Event(title="check").as_resource()
command = buildLaunchCommand([], res)

launcher.launch(oebs.project, command)
```

Deb package: python-pipeline-api

