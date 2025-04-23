# Кастомизация skotty

Этот раздел описывает структуру конфигурационного файла и его возможности.
Для унификации со всеми платформами, Skotty вычитывает конфиг из `~/.skotty/config.yaml`. Он бы мог поддерживать различные стандарты (e.g. [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/latest/) для GNU/Linux), но это сильно осложняет поддержку.

## Полный конфиг, со всеми возможными значениями {#full-config}
```yaml
# Путь к SSH-agent логу
agent_log_path: /path/to/agent.log
# Путь к управляющему сокету, на котором слушает gRPC сервис для управления skotty
# Спека: https://a.yandex-team.ru/arc_vcs/security/skotty/skotty/pkg/skottyctl/skottyrpc/service.proto
ctl_socket_path: /path/to/ctl.sock
# Изначально PIV предполагает работу с x509 сертификатами,
# поэтому skotty откладывает публичные части SSH сертификатов в эту директорию
ssh_keys_path: /path/to/skotty/pubs
# Список SSH-agent сокетов и их настроки, которые будет слушать skotty
sockets:
  # Имя сокета
- name: default
  # Тип сокета, возможные значения:
  #  - unix - обычный unix domain socket
  #    Единственный, который поддерживается в macOS, GNU/Linux и Windows
  #
  #  - cygwin - windows-specific сокет, реализующий Cygwin эмуляцию Unix сокетов
  #    Используется, как можно догадаться, в cygwin :)
  #
  #  - pageant - windows-specific сокет, реализующий Pageant протокол (реализует оба протокола).
  #    Если вы хотите явно обозначить реализацию, используйте pageant-pipe или pagean-window
  #
  #  - pageant-pipe - windows-specific сокет, реализующий Pageant протокол поверх named pipe
  #
  #  - pageant-window - windows-specific сокет, реализующий Pageant протокол поверх WM_COPYDATA
  #    Формально это legacy реализация putty <--> pageant взаимодействия и большая часть клиентов
  #    уже отказались от неё.
  #
  #  - pipe - windows-specific сокет, реализующий OpenSSH agent протокол поверх named pipes
  #    Используется в Win32-OpenSSH, потихоньку проникает всюду (e.g. https://youtrack.jetbrains.com/issue/IDEA-277305)
  #
  #  - dummy - заглушка, для реализации множественного many-to-one конфигурации сокетов
  #
  kind: some_kind
  # Заставляет проксировать все запросы в сокет с указанным именем.
  # Важен для Windows, где жизнь без many-to-one конфигуации жуткая боль
  same_as: some_socket_name
  # Путь в unix сокету/named pipe, на котором будет слушать сокет
  path: /path/to/listen.sock
  # Нужно ли показывать нотификацию при использовании ключа
  notify_usage: true
  # Настройка подтверждения использования ключей (aналогично "ssh-add -c ...")
  # Возможные значения:
  #   - any - будет требоваться подтверждение для всех ключей
  #   - added - только для добавленных с помощью ssh-add
  #   - keyring - все ключи Yubikey
  confirm: any
  # Список ключей, которые попадут в сокет из "кейринга"
  # Возможные значения:
  #   - secure - сертификат, выписанные на Secure CA
  #   - insecure - сертификат, выписанные на Insecure CA
  #   - legacy - legacy RSA ключ
  #   - sudo - сертификат, использующийся для аутентификации в sudo
  keys:
  - secure
  - insecure
  - sudo
  - legacy
  # Порядок ключей, отдаваемых сокетом
  # Возможные значения:
  #   - added - ключи добавленные с помощью ssh-add
  #   - secure - сертификат, выписанные на Secure CA
  #   - insecure - сертификат, выписанные на Insecure CA
  #   - legacy - legacy RSA ключ
  keys_order:
  - added
  - insecure
  - legacy
  - secure
# Имя сокета по умолчанию, используется при:
#  - генерации shell-скрипта в команде "skotty ssh env"
#  - при настроеной горячей замене системного $SSH_AUTH_SOCK
ssh_auth_sock: default
# Подборка настроек запуска агента
startup:
  # Указывает на необходимость экспорта переменных окружения SSH_AUTH_SOCK/SSH_AGENT_PID
  # Под GNU/Linux используется "systemctl --user set-environment ..."
  # Под macOS используется "launchctl setenv ..."
  # Под Windows ничего не делает, ибо windows для бедных
  export_auth_sock: true
  # macOS специфичный костыль, для перезаписи системного $SSH_AUTH_SOCK
  # в качестве нового значения, будет выбран путь сокета,  указанному в настройке ssh_auth_sock
  replace_auth_sock: false
# Настройка "кейринга" (т.н. хранилища ключей)
# !! Все за исключением pin не рекомендуется трогать руками
keyring:
  # Тип кейринга, возможные значения:
  #  - yubikey
  #  - keychain
  #  - files
  type: yubikey
  # Yubikey-специфичные настройки
  yubikey:
    # Серийный номер Yubikey
    # Т.к. имя PIV reader не стабильно - skotty ищет ваш yubikey по серийному номеру
    serial: 12504971
    # Провайдер пина для работы с yubikey, возможные значения:
    #  - plain:<my_pin> - пин хранится в открытом виде
    #    Пример, для пина "123456":
    #    pin: plain:123456
    #
    #  - secret:<blob> - пин расшифровывается на ключе, полученном от machine id.
    #    Machine id обычно генерится один раз при установке системы.
    #    Для более удобной работы с этим типом пинов, есть команда "skotty passtool"
    #    Пример, для пина "123456" для _моей_ системы:
    #    secret:bbc5ed4511cc068051e7697400a5377f2a160efeffecd8eb5bbae79adbe22e04faa1:541c5dee74d2aaf3ef629d29c62c78f532241859a1c6166b1211aaac4a246e98
    #
    #  - pinentry:<pinenty-program> - пин запрашивается с помощью pinentry.
    #    Поддерживается любое приложение, реализующее протокол Assuan PINENTRY.
    #    Пример:
    #    pinentry:/bin/pinentry
    #
    #  - keychain:<service> - пин хранится в кейчейне.
    #    На текущий момент поддерживается только macOS.
    #    Пример:
    #    keychain:skotty
    #
    pin: <kind>:<config>
  # Список ключей кейчейна, никогда не трогайте его руками
  available_keys:
  - legacy
  - sudo
  - insecure
  - secure
  - renew
  # Информация необходимая для обновления сертификатов
  enroll_info:
    enrollment_id: 20dc57f5-1c5a-45f6-adfe-84922185fbf4
    token_serial: "12504971"
    user: buglloc
# Настройка программы для подтверждения использования ключа
confirm:
  # Тип приложения, возможные значения:
  #  - ssh-askpass - приложение реализует ssh-askpass like протокол,
  #    т.е. выводит сообщение и выходит с 0 при согласии
  #
  #  - pinentry - приложение реализует протокол Assuan PINENTRY.
  #    (минимально необходима команда "GETPIN")
  #
  kind: ssh-askpass
  # Путь к приложению,
  # если оставить пустым - skotty пытается автоматически найти что-то подходящее
  program: <leave_empty_to_autodetect>
```

## Ручной ввод PIN {#pinentry}
Начиная с версии 0.9.9111584 вы можете сконфигурировать Skotty на запрос PIN при каждом запуске.
Для этого достаточно в конфиге изменить настройку `keyring.yubikey.pin`, указав там нужное вам приложение для запроса PIN. Приложение должно поддерживать [протокол Assuan PINENTRY](https://www.gnu.org/server/standards/translations/ru/gnupg/manual/pinentry/pinentry.html#toc-Protokol-Assuan-PINENTRY) и, как минимум, поддерживать команду `GETPIN`.
К примеру, настроим использование [pinentry-mac](https://formulae.brew.sh/formula/pinentry-mac) в macOS:
```yaml
keyring:
  type: yubikey
  yubikey:
    serial: 15715412
    pin: pinentry:pinentry-mac
```

В действии:
![pinentry-mac](_assets/skotty_pinentry-mac.png)

{% note warning %}

Будьте осторожны с передачей не абсолютного пути. Учтите, что переменная окружения `PATH` у демона Skotty и в вашей текущей оболочке может сильно отличаться.

{% endnote %}

{% note warning %}

Под GNU/Linux, в зависимости от вашего окружения и способа запуска skotty (по умолчанию это user systemd unit), нужные переменные окружения для работы GUI приложенек могут отсутствовать. Их можно пробросить в skotty добавив вызов `skotty notify startup-tty` в подходящее место (i.e. когда wayland/x11 уже стартанул, например, в `~/.xinitrc`).

{% endnote %}

{% note warning %}

Если вы будете использовать `pinentry-mac`, то отключите сохранение PIN в Keychain по умолчанию:
```
defaults write org.gpgtools.common UseKeychain NO
```

У меня нет идей, почему авторы решили что взводить ее по умолчанию - хорошая идея.

{% endnote %}

## Подтверждение использование ключа {#confirm}

Начиная с версии 0.9.9111584 Skotty умеет запрашивать подтверждение использования ключа и по умолчанию ведет себя аналогично OpenSSH Agent:
  - skotty запрашивает подтверждение только при добавлении ключа с помощью `ssh-add -c ...`
  - для этого он смотрит в переменную окружения `SSH_ASKPASS` и берет указаный там путь, как программу для запроса подтверждения. Ожидается стандартное поведение, при котором приложение выводит сообщение и выходит с 0 при согласии
  - если же переменная `SSH_ASKPASS` пуста, то skotty пытается найти нечто подходящее самостоятельно (GNU/Linux only), на данный момент это:
    * `/usr/lib/ssh/ssh-askpass`
	  * `/usr/X11R6/bin/ssh-askpass`
	  * `/usr/libexec/openssh/ssh-askpass`
    * `ssh-askpass` в `PATH`
  - если ничего не нашлось или skotty запущен под macOS или Windows - запрос подписи пофейлится

Теперь возможные кастомизации:
### Кастомизация ssh-askpass program
Вы можете пожелать явным образом сконфигурировать Skotty на использование подходящей вам программы запроса подтверждения.
Для этого достаточно поправить в конфиге настройки `confirm`.
Это может быть как передача пути к приложению:
```yaml
confirm:
  kind: ssh-askpass
  program: /my/cool/ask-prog
```

Так и использование pinentry-совместимых приложений (минимально необходима поддержка команды `CONFIRM`):
```yaml
confirm:
  kind: pinentry
  program: /opt/homebrew/bin/pinentry-mac
```

{% note warning %}

Будьте осторожны с передачей не абсолютного пути. Учтите, что переменная окружения `PATH` у демона Skotty и в вашей текущей оболочке может сильно отличаться.

{% endnote %}

{% note warning %}

Под GNU/Linux, в зависимости от вашего окружения и способа запуска skotty (по умолчанию это user systemd unit), нужные переменные окружения для работы GUI приложенек могут отсутствовать. Их можно пробросить в skotty добавив вызов `skotty notify startup-tty` в подходящее место (i.e. когда wayland/x11 уже стартанул, например, в `~/.xinitrc`).

{% endnote %}

### Требовать подтверждение ключей при подписи в определенном сокете
В отличии от OpenSSH Agent, skotty может форсировать подтверждение, вне зависимости от того как добавлялся ключ.
Для этого:
  * выбираете нужный сокет в конфиге
  * добавляете ему параметр `confirm`, Возможные значения:
    - `any` - будет требоваться подтверждение для всех ключей
    - `added` - только для добавленных с помощью ssh-add
    - `keyring` - все ключи Yubikey

Например, будем требовать подтвеждение для всех ключей:
```yaml
sockets:
- name: default
  kind: unix
  notify_usage: true
  confirm: any
  path: /home/buglloc/.skotty/sock/default.sock
  keys:
  - secure
  - insecure
  - sudo
  - legacy
```
В действии:
![linux-ssh-askpass](_assets/skotty_linux_ssh-askpass.png)

{% note warning %}

Под GNU/Linux, в зависимости от вашего окружения и способа запуска skotty (по умолчанию это user systemd unit), нужные переменные окружения для работы GUI приложенек погут отсутствовать. Их можно пробросить в skotty добавив вызов `skotty notify startup-tty` в подходящее место (i.e. когда wayland/x11 уже стартанул, например, в `~/.xinitrc`).

{% endnote %}

## Уведомления о использовании ключа {#notify_usage}

Технически, уведомления о использовании тех или иных ключей привязаны к конкретному сокету. Поэтому если вы устали от них (или соскучились), у вас есть две опции:
  - глобально включить/отключить их для всех сокетов, для этого достаточно вызвать `skotty setup --sockets` и правильно ответить на вопрос "Enable usage notifications?"
  - включить/отключить уведомления для нужного сокета (например, можно завести отдельный сокет только для форвардинга). Для этого нужно покрутить поле `notify_usage` (см. [полный конфиг](https://docs.yandex-team.ru/skotty/howto-configure#full-config))

## Шэринг софтовых ключей
По умолчанию, софтовые ключи (i.e. добавленные в рантайме) не шарятся между разными сокетами. И если говорить о GNU/Linux или macOS, то это вполне логично и естественно. Но с Windows это накладывает ряд неудобств, например, если вы одновременно используете remote development в VSCode (использует Win32-OpenSSH) и OpenSSH в Cygwin, то добавлять свои кастомные ключи нужно в оба сокета. Поэтому Skotty умеет шарить хранилище ключей между сокетами с помощью специальной опции `same_as: <another_socket>`.
К примеру, для Windows дефолтная конфигурация выглядит следующим образом:
```
# ~/.skotty/config.yaml

sockets:
- name: default
  kind: dummy
  path: n/a
  keys:
  - secure
  - insecure
  - sudo
  - legacy
- name: default-wsl
  kind: unix
  same_as: default
  path: C:\Users\buglloc\.skotty\sock\default-wsl.sock
- name: default-pagent
  kind: pageant
  same_as: default
  path: n/a
- name: default-cygwin
  kind: cygwin
  same_as: default
  path: C:\Users\buglloc\.skotty\sock\default-cygwin.sock
- name: default-win32-openssh
  kind: pipe
  default: true
  same_as: default
  path: \\.\pipe\openssh-ssh-agent
- name: sudo-win32-openssh
  kind: pipe
  path: \\.\pipe\sudo-openssh-ssh-agent
  keys:
  - sudo
```

В соответствии с ней, Skotty:
  - создаст отдельный `sudo` сокет
  - создаст `dummy` сокет, содержащий весь набор хардварных ключей
  - и к нему четыре отдельных представления: `default-wsl`, `default-pagent`, `default-cygwin` и `default-win32-openssh`

Т.е. у нас получится следующая картинка:
```
default-wsl ===========\
default-pagent  ========\
                         |---> dummy
default-cygwin  ========/
default-win32-openssh =/

sudo-win32-openssh
```
Таким образом, добавив ключ в любой из `default-*` сокетов он прорастет во все из них (но не в `sudo` сокет):
[![пример шэринга ключей](_assets/skotty_key_share.png)](https://jing.yandex-team.ru/files/buglloc/skotty_key_share.png)

