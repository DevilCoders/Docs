В обычной конфигурации tmux может некорректно работать с ssh-agent. Чаще всего это проявляется в виде ошибки вроде такой:
```
svn: E170013: Unable to connect to a repository at URL 'svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia'
svn: E210002: To better debug SSH connection problems, remove the -q option from 'ssh' in the [tunnels] section of your Subversion configuration file
svn: E210002: Network connection closed unexpectedly
```
Для исправления этой проблемы нужно при переподключениях обновлять ссылку на ssh auth socket.

Решение
=======

В файле `~/.tmux.conf` на целевой машине должно быть:

```
set -g update-environment -r
# fix ssh agent when tmux is detached
setenv -g SSH_AUTH_SOCK $HOME/.ssh/ssh_auth_sock
```

В файле `~/.ssh/rc` на целевой машине должно быть:
```
#!/bin/bash

# Fix SSH auth socket location so agent forwarding works with tmux
if test "$SSH_AUTH_SOCK" ; then
  ln -sf $SSH_AUTH_SOCK ~/.ssh/ssh_auth_sock
fi
```
Файл `~/.ssh/rc` должен иметь права на запуск (`x`).

В файле `~/.bashrc` на целевой машине должно быть:
```
if [[ -z "$TMUX"  ]] && [ "$SSH_CONNECTION" != ""  ]; then
    tmux attach-session -t ssh_tmux || tmux new-session -s ssh_tmux
fi
```

На своей машине должен быть включен форвардинг ssh (флаг `-A` при соединении или `ForwardAgent yes` в `.ssh/config`).
