```
  _____  _                       _       _         
 |  __ \| |                     | |     | |        
 | |__) | |__   ___  _ __   ___ | |_ ___| | ____ _ 
 |  ___/| '_ \ / _ \| '_ \ / _ \| __/ _ \ |/ / _` |
 | |    | | | | (_) | | | | (_) | ||  __/   < (_| |
 |_|    |_| |_|\___/|_| |_|\___/ \__\___|_|\_\__,_|
```

*Phonoteka* is *Yandex Verticals* service which keeps metadata by phones.

#### Projects wiki
https://wiki.yandex-team.ru/vertis/phonoteka/


#### Structure
  * `core` - dao, services, clients
  * `api ` - api
  * `tms`  - scheduler


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

    `./changes.sh` - add new version to changelog


#### git-hooks
To enable git hooks you need to cd to `<project directory>/hooks` and run  
`chmod +x setup-git-hooks.sh && ./setup-git-hooks.sh`


If you need to update hooks, just run `./setup-git-hooks.sh` after pulling changes from github.

When you perform `git commit` with pre-commit scalafmt hook, changes you've made are commited first, and then scalafmt is started. If scalafmt makes changes, style fixes will be committed automatically.
