# Настройка SSH: клиентская часть
Для начала, вам нужно выбрать одну из двух возможных конфигураций:
  - lightweight: без поддержки аутентификации в sudo
  - sudo forward: с поддержкой аутентификации в sudo

Конфигурация с поддержкой аутентификации в sudo немного сложнее (и возможно потребует обновления OS), но требуется для использования "парольного" sudo __на серверах__. Если же у вас не используется парольное sudo на серверах (например, вы ходите только в контейнеры Nanny/Deploy и собственные QYP-виртуалки), то можете воспользоваться упрощенной конфигурацией.

## lightweight конфигурация {#lightweight-config} {#zamena-shtatnogo-ssh-agenta}
Суть конфигурации заключается в том, чтобы система и SSH-клиент использовали Skotty по умолчанию. После этого вы сможете ходить на сервера по SSH, пользоваться `ya` и остальным тулингом, которому нужен доступ к SSH ключам.

Проверить, какой из SSH-агентов будет использовать SSH довольно легко, достаточно позвать `ssh-add -l`:
```
% ssh-add -l                                          
256 SHA256:bi87q8W5hbdWOl/olIE+BmHVCUKp64DjVe85Qwg1O4c Skotty key insecure on Yubikey (ECDSA-CERT)
2048 SHA256:ytOKQUEqcXkfdsdlO/UCgZ4QbICrwJ6jHtFWiJcdZqs Skotty key legacy on Yubikey (RSA)
256 SHA256:GVZ1iXiM/7poYBa8z8SjkY6Em6ph9Lv9PZmzsJVoBxQ Skotty key secure on Yubikey (ECDSA-CERT)
```
Если в выводе есть ключи от Skotty, значит скорее всего все хорошо и можно попробовать сходить на специальный отладочный SSH-сервер (ssh может запросить подтверждение доверию хостовому ключу, соглашаемся):
```
% ssh skotty.sec.yandex.net
Welcome to the Skotty Validation server.
Info about your connection:
  - Username: buglloc
  - Auth keys: 2
    * SHA256:bi87q8W5hbdWOl/olIE+BmHVCUKp64DjVe85Qwg1O4c
      - type: ecdsa-sha2-nistp256-cert-v01@openssh.com
      - present on staff: yes
      - revoked: no
      - principals: buglloc
      - valid before: 2022-09-18T12:28
      - ca fingerprint: SHA256:9PsYUcGRMBPVEHlt5gZYXduP7fCceJ7BVnoV3NsXZsA
      - serial: 1655717332857410781
      - key id: skotty:insecure:buglloc:y12504968:5b4789a6-6d36-4a81-a762-5c923fcf82e0
    * SHA256:GVZ1iXiM/7poYBa8z8SjkY6Em6ph9Lv9PZmzsJVoBxQ
      - type: ecdsa-sha2-nistp256-cert-v01@openssh.com
      - present on staff: yes
      - revoked: no
      - principals: buglloc
      - valid before: 2022-09-18T12:28
      - ca fingerprint: SHA256:9iugZLu67ykk8KutH/wJPudHxT4PismFrfy9ehLXOms
      - serial: 1655717332903808222
      - key id: skotty:secure:buglloc:y12504968:5b4789a6-6d36-4a81-a762-5c923fcf82e0
  - Agent forwarded: no

Have a great day! ;)
Connection to skotty.sec.yandex.net closed.
```

Если же `ssh-add -l` не вывел нужные ключи, то нужно предпринять шаги, зависящие от вашей платформы:

  {% list tabs %}

  - GNU/Linux

    Как вы знаете, разнообразие окружений в GNU/Linux велико, поэтому, для начала, обозначим целевое состояние - в переменной окружения `SSH_AUTH_SOCK` должен быть путь к сокету Skotty и она должна прорасти для всех приложений (i.e. не только в шелле). Например:
    ```
    $ env | grep SSH_AUTH_SOCK
    SSH_AUTH_SOCK=/home/buglloc/.skotty/sock/default.sock
    ```

    Для этого skotty пытается обновить переменные окружения с помощью `systemctl --user set-environment` и `dbus-update-activation-environment --systemd`, но это работает не во всех конфигурациях + может быть подвержено гонкам, если запускается несколько systemd-юнитов, которые пытаются установить `SSH_AUTH_SOCK` :)

    Поэтому ниже будут рецепты, которые удалось собрать:
    #### Если пользуетесь GNOME Keyring (Ubuntu, Xubuntu и типовые Gnome окружения)
    В Ubuntu может работать два ssh-агента:
      - `gnome-keyring-ssh`, запускаемый как systemd unit
      - ванильный `ssh-agent`, запускаемый в X11 сессии

    Предлагается на всякий случае отключить оба. Для этого:
      - отключаем автозапуск `gnome-keyring-ssh`:
      ```
      $ mkdir -p ~/.config/autostart/
      $ (cat /etc/xdg/autostart/gnome-keyring-ssh.desktop; echo X-GNOME-Autostart-enabled=false; echo Hidden=true) > ~/.config/autostart/gnome-keyring-ssh.desktop
      ```
      - отключаем запуск ванильного ssh-агента:
      ```
      $ sudo sed -i -e "s/^use-ssh-agent/#use-ssh-agent/g" /etc/X11/Xsession.options
      ```

    После этого перезагружаемся для проверки.

    #### Если у вас ssh-agent стартует X11 (Kubuntu, Lubuntu и типовые KDE окружения)
    Для этих окружений проще всего отключить Xsession опцию `use-ssh-agent`:
    ```
    $ sudo sed -i -e "s/^use-ssh-agent/#use-ssh-agent/g" /etc/X11/Xsession.options
    ```

    После этого перезагружаемся для проверки.

    #### Во всех остальных случаях
    Если вам нужна только консоль, то можно добавить вызов `skotty ssh env` в rc-файл вашего шелла (`~/.bashrc`/`~/.zshrc`/`etc`), например для `bash`:
    ```
    $ echo 'eval $(skotty ssh env)' >> ~/.bashrc
    $ source ~/.bashrc
    ```

    Если нужно, чтобы десктопные приложения так же гарантированно использовали сокет Skotty, то почитайте доку к вашему дистрибутиву или окружению рабочего стола. С большой долей вероятности там будет рассказано и как отключить штатный SSH-агент и как определить нужные переменные окружения.
    Хорошие точки для старта:
      - [Ubuntu: Session-wide environment variables](https://help.ubuntu.com/community/EnvironmentVariables#Session-wide_environment_variables)
      - [Arch Linux: Per user environment variables](https://wiki.archlinux.org/title/environment_variables#Per_user)

  - macOS

    В macOS все должно работать из коробки. Если говорить детальнее, то Skotty сам экспортирует переменные окружения с помощью `launchctl setenv` и это работало бы хорошо, если бы не штатный SSH-агент от эпла, который нельзя ни отключить (без отключения SIP и прочих шаманств) ни переопределить переменную окружения `SSH_AUTH_SOCK`. Поэтому Skotty применяет общеизвестный костыль и подменяет во время своей работы оригинальный сокет на собственный.

    Если же `ssh-add -l` не показывает ключи от Skotty, то скорее всего у вас где-то запускается еще один SSH-агент, который перетирает переменную окружения `SSH_AUTH_SOCK` и это нужно залечить. Этим, например, грешит Oh My Zsh.
    Ожидаемая диагностика при корректной переменной окружения `SSH_AUTH_SOCK`:
    ```
    % ls -la $SSH_AUTH_SOCK
    lrwxr-xr-x  1 buglloc  wheel  40 Jun 22 10:34 /private/tmp/com.apple.launchd.GSEpNMq947/Listeners -> /Users/buglloc/.skotty/sock/default.sock

    % lsof $(readlink $SSH_AUTH_SOCK)
    COMMAND   PID    USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
    skotty  52368 buglloc   11u  unix 0xe901a81a4c124c8f      0t0      /Users/buglloc/.skotty/sock/default.sock
    ```
    И пример, когда используется какой-то инородный сокет:
    ```
    % ls -la $SSH_AUTH_SOCK
    srw-------  1 buglloc  staff  0 Jul 14 14:03 /var/folders/qj/dnt80j9j5ls3jtt67qv5v11w0000gn/T//ssh-IwYGIDQ1PGFa/agent.69417

    % lsof /var/folders/qj/dnt80j9j5ls3jtt67qv5v11w0000gn/T//ssh-IwYGIDQ1PGFa/agent.69417
    COMMAND     PID    USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
    ssh-agent 69418 buglloc    3u  unix 0xe901a81a4c118faf      0t0      /var/folders/qj/dnt80j9j5ls3jtt67qv5v11w0000gn/T//ssh-IwYGIDQ1PGFa/agent.69417
    ```

  - Windows

    #### Putty
    Putty версии 0.76 и выше должен подхватить ключи по Pageant протоколу без дополнительных настроек. Достаточно выключить Pageant (если был запущен) и запустить Skotty.

    #### Win32-OpenSSH
    В named pipe `\\.\pipe\openssh-ssh-agent` ходит как штатный SSH-клиент в Windows, так и некоторые сторонние (новые версии IDE от JetBrains, VSCode, etc). Все должно работать из коробки, при условии что выключен Win32-OpenSSH Agent.
    Подробнее про отключение Win32-OpenSSH Agent: [socket/pipe already exist](https://docs.yandex-team.ru/skotty/troubleshooting#socket-used)

    #### Git
    Git for Windows живет собственной жизнью и использует встроенный SSH клиент вместо системного. Следствием этого могут быть разнообразные чудеса не совместимости при конфигурировании SSH клиента, т.к. читают они один и тот же конфиг, но работают по разному. Проще всего решить эту проблему - использовать Win32 OpenSSH при работе с git. Для этого достаточно:
    ```
    # Определить путь к ssh клиенту
    C:\Users\buglloc>where ssh
    C:\Program Files\OpenSSH\ssh.exe

    # заиспользовать его в git
    C:\Users\buglloc>git config --global core.sshCommand "C:/Program\ Files/OpenSSH/ssh.exe"
    ```

    После этого git for windows начнет использовать Win32 OpenSSH.

    #### WSL
    Для WSL необходимо переопределить переменную окружения `SSH_AUTH_SOCK` *в Ubuntu* (т.е. на дочерней системе, а не хостовой). Для этого достаточно поправить rc-файл вашего шелла (`~/.bashrc`/`~/.zshrc`/`etc`).
    Например, для bash (где `<username>` - ваш логин):
    ```
    $ echo 'export SSH_AUTH_SOCK="/mnt/c/Users/<username>/.skotty/sock/default-wsl.sock"' >> ~/.bashrc
    $ source ~/.bashrc
    ```

    #### WSL2
    WSL2 довольно сломанная штука и не имеет удобного интеропа для named pipes/unix-сокетов между WSL2 и Windows. Поэтому единственный надежный вариант - проксирование с помощью [wsl2proxy](https://docs.yandex-team.ru/skotty/how-it-works-wsl2#wsl2proxy), используя магию WSLInterop.
    Все действия будем производить в WSL2:
      - устанавливаем `wsl2proxy`:
      ```
      $ sudo tee -a /etc/apt/sources.list.d/yandex.list <<EOF
      deb http://common.dist.yandex.ru/common stable/all/
      deb http://common.dist.yandex.ru/common stable/amd64/
      EOF
      $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7FCD11186050CD1A
      $ sudo apt update && sudo apt -y install yandex-archive-keyring
      $ sudo apt install yandex-wsl2proxy
      ```
      - добавляем в rc-файл вашего шелла (`~/.bashrc`/`~/.zshrc`/`etc`) запуск прокси и установку переменных окружения:
      ```
      $ echo 'eval $(wsl2proxy start)' >> ~/.bashrc
      $ source ~/.bashrc
      ```
      - можем проверять:
      ```
      $ ssh-add -l
      256 SHA256:Eej4ul5e9a63E7tga9f+JCjeNROia7WOgZb4x1nhbB4 Skotty key insecure on Yubikey (ECDSA-CERT)
      2048 SHA256:tOd2ARtWi3XYiAHG4gfKqhehiJnsURZYXpSPWdKmP70 Skotty key legacy on Yubikey (RSA)
      256 SHA256:J8O81/usF9JX27nFrz9tDF1QpWcLn9wxlxqb1h5ut4g Skotty key secure on Yubikey (ECDSA-CERT)
      ```
    P.S. Важно отметить, что поддержка WSL2 довольно свежа. Если у вас возникнут какие-то проблемы/идеи по улучшению - не сдерживайте себя.

  {% endlist %}

  Если после всех проделанных манипуляций все еще ничего не выходит, смело приходите в [чатик](https://skotty.sec.yandex-team.ru/support/telegram) - посмотрим, подскажем, поможем.

## sudo forward конфигурация {#sudo-forward-config}

{% note warning %}

Перед тем как приступить к этой конфигурации, проделайте [предыдущую](#lightweight-config).

{% endnote %}

Эта конфигурация предполагает, что у вас используется "парольное" sudo на удаленных серверах. Т.к. теперь для аутентификации в sudo необходимо форвардить сокет ssh-agent, а пробрасывать его направо и налево [не безопасно](https://man.archlinux.org/man/ssh.1.en#A), предполагается использование двухсокетной конфигурации.
Для этого Skotty по-умолчанию создает два сокета:
  - один с полным набором ключей
  - второй только для работы с sudo

К сожалению, возможность такой конфигурации появилась только начиная с OpenSSH версии 8.2. Если у вас версия ниже (можно проверить с помощью `ssh -V`), то стоит предварительно запланировать обновление:
  - Ubuntu до Focal (обновит OpenSSH до версии 8.2)
  - macOS до Monterey (обновит OpenSSH до версии 8.6)
  - Windows предусматривает только [ручную установку Win32OpenSSH](https://docs.yandex-team.ru/skotty/howto-update-win32ssh)

{% note warning %}

Обновление до OpenSSH 8.8+ [ломает](https://confluence.atlassian.com/bitbucketserverkb/ssh-rsa-key-rejected-with-message-no-mutual-signature-algorithm-1026057701.html) работу с Bitbucket, чинится разрешением использования устаревшей `RSA SHA-1` подписи для нужного хоста в конфиге `~/.ssh/config`.
  ```
  Host bb.yandex-team.ru
    PubkeyAcceptedKeyTypes +ssh-rsa
  ```

{% endnote %}

Дальнейшая настройка зависит от вашей платформы:
  {% list tabs %}

  - GNU/Linux и macOS

    Для начала, проверим какие сокеты настроены в Skotty:
    ```
    $ skotty info
    --- Skotty ---
    Version: 0.9.0

    --- Agent ---
    Log: /home/buglloc/.skotty/logs/agent.log
    Status: OK (pid: 4154)

    --- Sockets ---
    + default (default)
      - path: /home/buglloc/.skotty/sock/default.sock
      - kind: unix
      - keys: secure + insecure + sudo + legacy
    + sudo
      - path: /home/buglloc/.skotty/sock/sudo.sock
      - kind: unix
      - keys: sudo

    --- Keyring ---
    Kind: Yubikey
    Serial: 15715313
    PIN: ******

    --- Keys ---
    + legacy
    + sudo
    + insecure
    + secure
    ```

    Затем настраиваем SSH клиент таким образом, чтобы форвардить сокет содержащий все ключи (`default` в примере выше) только на хосты, которые должны всегда иметь полный набор ключей (e.g. dev-виртуалки `my-cool.dev.host.yandex.net`, `my-cool1.dev.host.yandex.net` в примере ниже). А на все остальные "пустой" сокет пригодный только для аутентификации в sudo. Skotty умеет подсказывать вам пример такой конфигурации, но никак не ограничивает ваш полёт фантазии:
    ```
    $ skotty ssh conf
    # Sample ~/.ssh/config

    Host my-cool.dev.host.yandex.net my-cool1.dev.host.yandex.net
      # Forward default sock to the remote dev machine
      ForwardAgent %d/.skotty/sock/default.sock


    Host *.yandex.net
      # Forward only "sudo" socket to the untrusted environment
      ForwardAgent %d/.skotty/sock/sudo.sock
      # But authenticate through default socket
      IdentityAgent %d/.skotty/sock/default.sock
    ```
    Это пример дефолтной конфигурации, которую нужно сохранить в `~/.ssh/config`.

    Проверить конфигурацию можно походом на специальный SSH сервер `skotty.sec.yandex.net` (добавились поля `Agent forwarded: yes` и `Agent support sudo: yes` в отличии от lightweight конфигурации):
    ```
    % ssh skotty.sec.yandex.net
    Welcome to the Skotty Validation server.
    Info about your connection:
      - Username: buglloc
      - Auth keys: 2
        * SHA256:bi87q8W5hbdWOl/olIE+BmHVCUKp64DjVe85Qwg1O4c
          - type: ecdsa-sha2-nistp256-cert-v01@openssh.com
          - present on staff: yes
          - revoked: no
          - principals: buglloc
          - valid before: 2022-09-18T12:28
          - ca fingerprint: SHA256:9PsYUcGRMBPVEHlt5gZYXduP7fCceJ7BVnoV3NsXZsA
          - serial: 1655717332857410781
          - key id: skotty:insecure:buglloc:y12504968:5b4789a6-6d36-4a81-a762-5c923fcf82e0
        * SHA256:GVZ1iXiM/7poYBa8z8SjkY6Em6ph9Lv9PZmzsJVoBxQ
          - type: ecdsa-sha2-nistp256-cert-v01@openssh.com
          - present on staff: yes
          - revoked: no
          - principals: buglloc
          - valid before: 2022-09-18T12:28
          - ca fingerprint: SHA256:9iugZLu67ykk8KutH/wJPudHxT4PismFrfy9ehLXOms
          - serial: 1655717332903808222
          - key id: skotty:secure:buglloc:y12504968:5b4789a6-6d36-4a81-a762-5c923fcf82e0
      - Agent forwarded: yes
      - Agent support sudo: yes
      - Agent keys: 0

    Have a great day! ;)
    Connection to skotty.sec.yandex.net closed.
    ```

  - Windows (Win32-OpenSSH)

    Для начала, проверим какие сокеты настроены в Skotty:
    ```
    λ skotty info
    --- Skotty ---
    Version: 0.9.0

    --- Agent ---
    Log: C:\Users\buglloc\.skotty\logs\agent.log
    Status: OK (pid: 3124)

    --- Sockets ---
    + default-wsl
      - path: C:\Users\buglloc\.skotty\sock\default-wsl.sock
      - kind: unix
      - keys: secure + insecure + sudo + legacy
    + default-pagent
      - path: n/a
      - kind: pageant
      - keys: secure + insecure + sudo + legacy
    + default-cygwin
      - path: C:\Users\buglloc\.skotty\sock\default-cygwin.sock
      - kind: cygwin
      - keys: secure + insecure + sudo + legacy
    + default-win32-openssh (default)
      - path: \\.\pipe\openssh-ssh-agent
      - kind: pipe
      - keys: secure + insecure + sudo + legacy
    + sudo-win32-openssh
      - path: \\.\pipe\sudo-openssh-ssh-agent
      - kind: pipe
      - keys: sudo

    --- Keyring ---
    Kind: Files
    Base path: C:\Users\buglloc\.skotty\filering
    Passphrase: ********************************

    --- Keys ---
    + legacy
    + sudo
    + insecure
    + secure
    ```

    Затем настраиваем SSH клиент таким образом, чтобы форвардить сокет содержащий все ключи (`default-win32-openssh` в примере выше) только на хосты, которые должны всегда иметь полный набор ключей (e.g. dev-виртуалки `my-cool.dev.host.yandex.net`, `my-cool1.dev.host.yandex.net` в примере ниже). А на все остальные "пустой" сокет пригодный только для аутентификации в sudo (`sudo-win32-openssh` в примере выше). Skotty умеет подсказывать вам пример такой конфигурации, но никак не ограничивает ваш полёт фантазии (не забудте заменить `<your-login-here>` на ваш логин на стаффе):

    ```
    λ skotty ssh conf
    # Sample ~/.ssh/config
    # This configuration is generated for Win32-OpenSSH v8.6.0+. If you are using a different client, you must configure it manually: (

    User <your-login-here>

    Host my-cool.dev.host.yandex.net my-cool1.dev.host.yandex.net
      # Forward default sock to the remote dev machine
      ForwardAgent //./pipe/openssh-ssh-agent


    Host *.yandex.net
      # Forward only "sudo" socket to the untrusted environment
      ForwardAgent //./pipe/sudo-openssh-ssh-agent
      # But authenticate through default socket
      IdentityAgent //./pipe/openssh-ssh-agent
    ```

    Проверить конфигурацию можно походом на специальный SSH сервер `skotty.sec.yandex.net` (добавились поля `Agent forwarded: yes` и `Agent support sudo: yes` в отличии от lightweight конфигурации):
    ```
    λ ssh skotty.sec.yandex.net
    Welcome to the Skotty Validation server.
    Info about your connection:
      - Username: buglloc
      - Auth keys: 3
        * SHA256:8dUj7K47D0deZw03+CJvBqG7D4lbZ7aZuFk9oMiX7XE
          - type: ecdsa-sha2-nistp256-cert-v01@openssh.com
          - present on staff: yes
          - revoked: no
          - principals: buglloc
          - valid before: 2022-07-12T11:03
          - ca fingerprint: SHA256:9PsYUcGRMBPVEHlt5gZYXduP7fCceJ7BVnoV3NsXZsA
          - serial: 1649837023603483872
          - key id: skotty:insecure:buglloc:y12504971:3b38b2a5-2e1b-4059-b880-86e42baf978a
        * SHA256:ToTU2NxQjKDZr2L8/OTxCnzCGqk5GUPlLht3WhgWJKY
          - type: ssh-rsa
          - present on staff: yes
        * SHA256:iBa0aivK9MBw2FLCbInzV0zMj+3Kf7Y9MDRN3j6jc8U
          - type: ecdsa-sha2-nistp256-cert-v01@openssh.com
          - present on staff: yes
          - revoked: no
          - principals: buglloc
          - valid before: 2022-07-12T11:03
          - ca fingerprint: SHA256:9iugZLu67ykk8KutH/wJPudHxT4PismFrfy9ehLXOms
          - serial: 1649837023633935205
          - key id: skotty:secure:buglloc:y12504971:3b38b2a5-2e1b-4059-b880-86e42baf978a
      - Agent forwarded: yes
      - Agent support sudo: yes
      - Agent keys: 0

    Have a great day! ;)
    ```

  - Windows (WSL)

    В этом разделе речь идет о настройке именно WSL (не WSL2, который имеет мало общего с сабжем).

    Настраиваем SSH клиент таким образом, чтобы форвардить сокет содержащий все ключи (т.н. `default-wsl`) только на хосты, которые должны всегда иметь полный набор ключей (e.g. dev-виртуалки `my-cool.dev.host.yandex.net`, `my-cool1.dev.host.yandex.net` в примере ниже). А на все остальные "пустой" сокет пригодный только для аутентификации в sudo (т.н. `sudo-wsl`). Например (не забудьте заменить `<username>` на ваш логин):
    ```
    $ cat ~/.ssh/config
    Host my-cool.dev.host.yandex.net my-cool1.dev.host.yandex.net
      # Forward default sock to the remote dev machine
      ForwardAgent /mnt/c/Users/<username>/.skotty/sock/default-wsl.sock


    Host *.yandex.net
      # Forward only "sudo" socket to the untrusted environment
      ForwardAgent /mnt/c/Users/<username>/.skotty/sock/sudo-wsl.sock
      # But authenticate through default socket
      IdentityAgent /mnt/c/Users/<username>/.skotty/sock/default-wsl.sock
    ```

    Проверить конфигурацию можно походом на специальный SSH сервер `skotty.sec.yandex.net` (добавились поля `Agent forwarded: yes` и `Agent support sudo: yes` в отличии от lightweight конфигурации):
    ```
    buglloc@bugbuggy:~$ ssh skotty.sec.yandex.net
    Welcome to the Skotty Validation server.
    Info about your connection:
      - Username: buglloc
      - Auth keys: 3
        * SHA256:8dUj7K47D0deZw03+CJvBqG7D4lbZ7aZuFk9oMiX7XE
          - type: ecdsa-sha2-nistp256-cert-v01@openssh.com
          - present on staff: yes
          - revoked: no
          - principals: buglloc
          - valid before: 2022-07-12T11:03
          - ca fingerprint: SHA256:9PsYUcGRMBPVEHlt5gZYXduP7fCceJ7BVnoV3NsXZsA
          - serial: 1649837023603483872
          - key id: skotty:insecure:buglloc:y12504971:3b38b2a5-2e1b-4059-b880-86e42baf978a
        * SHA256:ToTU2NxQjKDZr2L8/OTxCnzCGqk5GUPlLht3WhgWJKY
          - type: ssh-rsa
          - present on staff: yes
        * SHA256:iBa0aivK9MBw2FLCbInzV0zMj+3Kf7Y9MDRN3j6jc8U
          - type: ecdsa-sha2-nistp256-cert-v01@openssh.com
          - present on staff: yes
          - revoked: no
          - principals: buglloc
          - valid before: 2022-07-12T11:03
          - ca fingerprint: SHA256:9iugZLu67ykk8KutH/wJPudHxT4PismFrfy9ehLXOms
          - serial: 1649837023633935205
          - key id: skotty:secure:buglloc:y12504971:3b38b2a5-2e1b-4059-b880-86e42baf978a
      - Agent forwarded: yes
      - Agent support sudo: yes
      - Agent keys: 0

    Have a great day! ;)
    ```

  - Windows (WSL2)

    В этом разделе речь идет о настройке именно WSL2 (не WSL1, который имеет мало общего с сабжем).

    После того как вы настроили wsl2proxy, у вас должно быть две переменные окружения с двумя разными сокетами:
    ```
    $ env | grep 'SSH.*SOCK'
    SSH_AUTH_SOCK=/tmp/wsl2proxy-buglloc/default-ssh-auth.sock
    SSH_SUDO_AUTH_SOCK=/tmp/wsl2proxy-buglloc/sudo-ssh-auth.sock
    ```

    Настраиваем SSH клиент таким образом, чтобы форвардить сокет содержащий все ключи (`SSH_AUTH_SOCK`) только на хосты, которые должны всегда иметь полный набор ключей (e.g. dev-виртуалки `my-cool.dev.host.yandex.net`, `my-cool1.dev.host.yandex.net` в примере ниже). А на все остальные "пустой" сокет пригодный только для аутентификации в sudo (`SSH_SUDO_AUTH_SOCK`). Например (не забудьте заменить пути к сокетам на пути из вашего окружения!):
    ```
    $ cat ~/.ssh/config
    Host my-cool.dev.host.yandex.net my-cool1.dev.host.yandex.net
      # Forward default sock to the remote dev machine
      ForwardAgent /tmp/wsl2proxy-buglloc/default-ssh-auth.sock

    Host *.yandex.net
        # Forward only "sudo" socket to the untrusted environment
        ForwardAgent /tmp/wsl2proxy-buglloc/sudo-ssh-auth.sock
        # But authenticate through default socket
        IdentityAgent /tmp/wsl2proxy-buglloc/default-ssh-auth.sock
    ```
    Note: В OpenSSH v8.4+ можно использовать переменные окружения, вместо хардкода, но его пока не завезли в Ubuntu Focal.

    Проверить конфигурацию можно походом на специальный SSH сервер `skotty.sec.yandex.net` (добавились поля `Agent forwarded: yes` и `Agent support sudo: yes` в отличии от lightweight конфигурации):
    ```
    buglloc@bugbuggy:~$ ssh skotty.sec.yandex.net
    Welcome to the Skotty Validation server.
    Info about your connection:
      - Username: buglloc
      - Auth keys: 3
        * SHA256:Eej4ul5e9a63E7tga9f+JCjeNROia7WOgZb4x1nhbB4
          - type: ecdsa-sha2-nistp256-cert-v01@openssh.com
          - present on staff: yes
          - revoked: no
          - principals: buglloc
          - valid before: 2022-10-05T19:38
          - ca fingerprint: SHA256:9PsYUcGRMBPVEHlt5gZYXduP7fCceJ7BVnoV3NsXZsA
          - serial: 1657211934348461557
          - key id: skotty:insecure:buglloc:y15715313:ca882c07-5572-4e7e-8fc0-9ccaaaa3750a
        * SHA256:tOd2ARtWi3XYiAHG4gfKqhehiJnsURZYXpSPWdKmP70
          - type: ssh-rsa
          - present on staff: yes
        * SHA256:J8O81/usF9JX27nFrz9tDF1QpWcLn9wxlxqb1h5ut4g
          - type: ecdsa-sha2-nistp256-cert-v01@openssh.com
          - present on staff: yes
          - revoked: no
          - principals: buglloc
          - valid before: 2022-10-05T19:38
          - ca fingerprint: SHA256:9iugZLu67ykk8KutH/wJPudHxT4PismFrfy9ehLXOms
          - serial: 1657211934388858864
          - key id: skotty:secure:buglloc:y15715313:ca882c07-5572-4e7e-8fc0-9ccaaaa3750a
      - Agent forwarded: yes
      - Agent support sudo: yes
      - Agent keys: 0

    Have a great day! ;)
    Connection to skotty.sec.yandex.net closed.
    ```

  {% endlist %}

  На этом все :)
