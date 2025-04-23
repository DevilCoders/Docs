*Techsupport* is *Yandex Verticals* techsupport service.


#### Projects wiki
https://wiki.yandex-team.ru/vertis/techsupport

#### git-hooks
To enable git hooks you need to cd to `<project directory>/hooks` and run  
`chmod +x setup-git-hooks.sh && ./setup-git-hooks.sh`


If you need to update hooks, just run `./setup-git-hooks.sh` after pulling changes from github.

When you perform `git commit` with pre-commit scalafmt hook, changes you've made are commited first, and then scalafmt is started. If scalafmt makes changes, style fixes will be committed automatically.
