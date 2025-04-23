Theatre is a library that helps to run async background routines.
Core ideas: 
* Provide reusable, composable schedules of diffirent kinds ([roles](roles) directory)
* Separate business logic from schedule algorithms, allowing to run same chunk of logic based on different system events
* Schedule providers decorate user-defined business logic with common helpful functionality like 
  - [profiling](profiling)
  - mixing [id of current routine](logging/request_id.py) to logger context
  - generating meaningful asyncio.Task name in case of 
  [nested tasks](utils/nested_job.py)
  or [inheritance from schedule role class](utils/derived_job.py)

As an example of app based on theatre, one can look at [DB stat collecting module](../../pg/mdb/python/cron/db_stats/main.py).

Contents:
* [roles](roles) - Collection of schedule algorithms for tasks like 
[run code every fixed time interval](roles/cron.py) or 
[run code for every item pushed to queue](roles/queue.py)
* [profiling](profiling) - Container for aggregation of success/fail/wait timings in histograms, compatible with Yasm
* [app](app) - Reusable helpers/boilerplate for building an app. Convenient in common cases, but totally optional
* [stages](stages) - Apps that are potentially reusable in diffirent services
* [detail](detail) - Boring implementation details
