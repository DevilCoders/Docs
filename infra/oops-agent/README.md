# OOPS agent

## modules
* oops-bootstrap.py
* oops-recipe.py
* oops-agent.py

### oops-bootstrap.py
runs by system cron every 5 minutes. Loads `oops-recipe.py`
from oops server and runs it.

#### Usage:

`oops-bootstrap.py [--server hostname] [--dir dirname]`

--server servername - set oops server address

--dir dirname - use `dirname` as work dir

### oops-recipe.py

Takes care about agent renew and start | stop

#### Usage:

`oops-recipe.py [--hostname hostname] [--server host] [--start | --stop | --status]`

--server servername - set oops server address

Auto mode (without [--start | --stop | --status]):

* uses directory with oops-recipe.py as work dir
* downloads `oops-agent.py` from oops server
* downloads `config.json` from oops server
* if config **or** agent.py changed **or** doesn't exist overwrites them and
restarts `oops-agent.py`
* if `oops-agent.py` isn't run (checks via oops-agent.pid) - runs it
* writes log to `oops-recipe.log`

Manual mode:

If [--start | --stop | --status] key is used, just starts | stops | checks 
`oops-agent.py` status


### oops-agent.py

#### Usage:

`oops-agent.py [-d] [--debug] [--hostname hostname] [--server servername]`

-d daemonize

--server servername - set oops server address

--hostname hostname - use `hostname` as agent hostname

--debug - write log to console & don't send smth. to server

* uses directory with oops-agent.py as work dir
* writes log to `oops-agent.log`
* writes pid to `oops-agent.pid`
* writes config to `running-config` on `SIG_USR1`
