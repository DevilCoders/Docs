# unsafe-robot-configurations

Finds all robots which operate in one DC:

`./unsafe-robot-configurations --env test`

And reconfigures then according to the given host pattern:

`./unsafe-robot-configurations --env test --reconfigure-host-pattern --reconfigure-host-pattern 'vla|sas'`
