# WSL2
Технически, WSL2 не поддерживает `AF_UNIX` интероп (см. [Windows/WSL AF_UNIX Interop doesn't work in WSL2](https://github.com/microsoft/WSL/issues/5961)) совсем :( Поэтому для того, чтобы сходить из WSL2 в named pipe/unix-сокет живущий в Windows применяют общепризнанный костыль с проксированием из WSL в:
  - `AF_VSOCK`. Требует, чтобы со стороны Windows кто-то полил появление новых виртуалок и пробрасывал в них hvsock, т.к. [WSL2 не поддерживает HV_GUID_WILDCARD ](https://github.com/microsoft/WSL/issues/5751)
  - pipe PE бинаря. Работает за счет магии WSLInterop, который позволяет подключаться PE бинарям к любому сокету в Windows (т.к. технически выполняется в хостовой системе, т.е. в Windows)

Т.к. первый вариант довольно хрупкий и багоопасный, выглядит разумее пойти вторым путем. Интернет предлагает скрещивать `socat` с `npiperelay`, но это какой-то слабо контролируемый путь, поэтому вместо этого был написан [wsl2proxy](https://a.yandex-team.ru/arcadia/security/skotty/wsl2proxy). Его основная задача - проксирование из WSL2 в named pipe для Win32OpenSSH в Windows.

## WSL2Proxy {#wsl2proxy}
`wsl2proxy` состоит из двух частей:
  - Linux бинаря, чтоб мочь забиндиться на Unix-сокет в WSL2
  - Windows бинаря, чтоб мочь подключиться к named pipe/unix-сокету в Windows

Таким образом, принцип работы довольно не хитер:
  - в linux мы слушаем нужные unix-сокеты
  - запускаем из под linux windows бинарь для форварда коннекта
  - мультиплексируем подключения через stdin/stdout пайпы

Для простоты, это можно изобразить следующим образом:
![wsl2proxy](_assets/wsl2proxy.svg)

## Как использовать
Достаточно запустить `wsl2proxy start`, который:
  - проверит существует ли уже запущенный инстанс
  - если нет, то запустит его фоновым процессом
  - распечатает в stdout переменные окружения с путями к сконфигурированным сокетам

Например:
```
buglloc@bugbuggy:~$ wsl2proxy start
SSH_AUTH_SOCK="/tmp/wsl2proxy-buglloc/default-ssh-auth.sock"; export SSH_AUTH_SOCK
SSH_SUDO_AUTH_SOCK="/tmp/wsl2proxy-buglloc/sudo-ssh-auth.sock"; export SSH_SUDO_AUTH_SOCK
```

## Конфигурирование WSL2Proxy
Помимо целей Skotty, WSL2Proxy в теории может использоваться для проксирования произвольного named pipe или unix-сокета из WSL2 в Windows. Для этого у него есть конфиг, который он зачитывает из `~/.config/wsl2proxy/config.yaml`. Разберем его на примере дефолтного конфига:
```yaml
# Уровень логирования
log_level: info
# Путь к логу
log_path: {runtime_dir}/proxy.log
# Путь к рабочему каталогу, по уполчанию берется или env[XDG_RUNTIME_DIR] или временный каталог
runtime_dir: /tmp/wsl2proxy-buglloc
# Набор сокетов
sockets:
  # Имя переменной окружения, в которое будет проставлен путь к сокету при запуске
- env_name: SSH_AUTH_SOCK
  # Путь к Unix-сокету в WSL2
  linux_addr: {runtime_dir}/default-ssh-auth.sock
  # Путь к pipe/unix сокету в Windows
  windows_addr: pipe://./pipe/openssh-ssh-agent
- env_name: SSH_SUDO_AUTH_SOCK
  linux_addr: {runtime_dir}/sudo-ssh-auth.sock
  windows_addr: pipe://./pipe/sudo-openssh-ssh-agent
```

P.S. После правок не забудьте перезапустить wsl2proxy
