Balancer Agent
=====

Balancer Agent is an L3 balancer's configuration management system. It is designed to automatically collect, test, deploy and rollback balancer's config. It works in conjunction with L3 API which provides tasks to agent and orchestates agent's behavior.

Installing
----------
...


A Simple Example
----------------

...

Configuration parameters
----------------
##### global settings
-  `stage` - defines agent's environment settings, including but not limited to logging settings, env variables and testing settings. 
Avaliable values - `production` `development` `test`.
Default - No defaults. Must be set in config

##### section [main]
###### The section for settings that don't change during agent's lifecycle
 - `agent_mode` - agent can be used for LB configuration testing or for production configuration deploy.
Avaliable values - `test` `production`.
Default - No defaults. Must be set in config

##### section [startup]
###### Startup settings that may be overridden by settings collected from L3
- `l3_hosts_pool` - a list of L3 host fqdns ["https://l3-test.tt.yandex-team.ru/api/v1/agent"]
- `initial_state` - defines agent's startup workflow, whether to stay silent - `IDLE` or to start polling tasks - `ACTIVE`
Avaliable values - `IDLE` `ACTIVE`
- `settings_polling_interval` - minimal interval for settings colection from L3 in milliseconds
Default - No defaults. Must be set in config
- `tasks_polling_interval` - minimal interval for tasks colection from L3 in milliseconds
Default - No defaults. Must be set in config
- `signal_failure_interval` - minimal interval for sending a failure report to L3 in milliseconds
Default - No defaults. Must be set in config

##### section [controller]
###### Settings for the main thread tracking agent's status
- `data_collector_url` - controller sends worker's status reports to that url. That is an L3 host at the moment, but this can be changed to data collector/monitoring system in the future.
Default - No defaults. Must be set in config
- `worker_tracking_seconds` - timer in seconds for worker status generation
Default - No defaults. Must be set in config

TODO: add desription for 'auth' section

Links
-----

- ###### Proposal: https://wiki.yandex-team.ru/users/piskunov-va/l3mgr-v2-agent/
- ###### L3 API docs: https://swagger-ui.yandex-team.ru/?url=https://rtnmgr-test.tt.yandex-team.ru/tmp/swagger