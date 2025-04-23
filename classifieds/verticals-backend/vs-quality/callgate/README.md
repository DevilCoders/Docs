```
_________        .__  .__                 __          
\_   ___ \_____  |  | |  |    _________ _/  |_  ____  
/    \  \/\__  \ |  | |  |   / ___\__  \\   __\/ __ \ 
\     \____/ __ \|  |_|  |__/ /_/  > __ \|  | \  ___/ 
 \______  (____  /____/____/\___  (____  /__|  \___  >
        \/     \/          /_____/     \/          \/ 
```

*Callgate* is *Yandex Verticals* call-center proxy service.


#### Projects wiki
https://wiki.yandex-team.ru/vertis/callgate/


#### Structure
  * `callgate-model` - domain model
  * `callgate-core` - dao, services, clients
  * `callgate-server` - logging, metered, monitored mixins
  * `callgate-api` - api
  * `callgate-tms` - scheduler, consumers


#### Build commands
  * Clean

    `make clean`
  * Compile

    `make {module-name}/compile`

    `make compile` - whole project
  * Test

    `make {module-name}/test`

    `make test` - whole project

  * Code auto format

    `make fmt`
  * Make release

    `./inc_version.sh {module-name}` - add new version to changelog
    
    
#### git-hooks
To enable git hooks you need to cd to `<project directory>/hooks` and run  
`chmod +x setup-git-hooks.sh && ./setup-git-hooks.sh`


If you need to update hooks, just run `./setup-git-hooks.sh` after pulling changes from github.

When you perform `git commit` with pre-commit scalafmt hook, changes you've made are commited first, and then scalafmt is started. If scalafmt makes changes, style fixes will be committed automatically.
