Hobo 
====

https://wiki.yandex-team.ru/vertis/hobo/

### How to deploy on development environment
You can deploy two components: `hobo-api` and/or `hobo-tms`

Add file `upload.properties` to the root project directory with only one property - `ssh.host` (address of your dev environment) <br>
For example, `ssh.host=user-myt-123.dev.vertis.yandex.net`

Let below `$MODULE` to be one of `hobo-api` or `hobo-tms` (depends on what do you want to deploy) <br>
Call maven command: <br>
`mvn clean install --projects $MODULE --also-make -Pdevelopment-deploy` <br>
That command will create `./dist/$MODULE` directory at specified environment

Go to your environment and make `cd ./dist/$MODULE` <br>
Then first of all you need to install all necessary dependencies. For that call `./initialize.sh` <br>
It may require root privileges

After that to start the application do `./start.sh`

#### git-hooks
To enable git hooks you need to cd to `<project directory>/hooks` and run
`chmod +x setup-git-hooks.sh && ./setup-git-hooks.sh`

If you need to update hooks, just run `./setup-git-hooks.sh` after pulling changes from github.
