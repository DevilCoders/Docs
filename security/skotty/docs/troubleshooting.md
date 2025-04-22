# Troubleshooting

В случае возникновения проблем нужно:
  - не паниковать
  - прочитать о возможных проблемых ниже
  - если ничего не помогло:
    1. собрать диагностику: `skotty dump debug`
    2. написать на [security@](mailto:security@yandex-team.ru) или в чатик [Oh My Yubikey (Skotty public chat)](https://t.me/+ga7UEj4gQ4JkZWUy) описав проблему
    3. приложить лог агента (`~/.skotty/logs/agent.log`) и отладочный лог из п1

### Skotty не видит Yubikey {#no-keyring-available}
Это может проявляться в разных ситуациях, например:
  - не работает `skotty setup`, выдавая ошибку: `no keyring available`
  - `skotty yubikey list` ничего не выводит
  - не работает подпись с ошибками в логе `~/.skotty/logs/agent.log` вида:
  ```
  open keyring tx: can't initialize yubikey: yubikey with serial 15715313 is not found
  ```

Чаще всего это происходит в трех случаях:
  - у вас "YubiKey 5 Nano Type A" и вы вставляйте его не правильной стороной :) Легко не заметить, серьезно
  - система не видит Yubikey как устройство
  - демон смарт-карт не считает Yubikey за смарт-карту

Если с первым случаем все понятно, то со остальными все несколько сложнее. Для диагностики можно попробовать:
  - убедиться видит ли система Yubikey как USB устройство
  - если не видит - попробовать вставить в другой порт или в другой ноутбук. Если ничего не помогло - нужно идти на welcome service desk :(
  - в противном случае - попробовать передернуть pcscd демон и вытащить/вставить Yubikey:
    * если у вас GNU/Linux: `sudo systemctl restart pcscd`
    * если у вас macOS: `sudo killall -9 ctkd; sudo killall -9 com.apple.ifdreader` 
  - если и это не помогло - соберите диагностику с помощью `skotty dump debug` и заводите тикет, будем смотреть вместе

### Забыл Yubikey
В случае, если вы забыли yubikey - можно получить временные сертификаты для in-memory хранилища и работать на них.
Для этого:
  1. останавливаем skotty:
    * GNU/Linux: `systemctl --user stop skotty`
	* macOS: `launchctl unload ~/Library/LaunchAgents/ru.yandex.skotty.plist`
	* Windows: `quit` в меню трея
  2. запускаем skotty с получением временных сертификатов: `skotty start --temporary`
  3. проходим web-аутентификацию
  4. skotty получает `secure` + `insecure` + `sudo` сертификаты на in-memory ключах и запускается

{% note warning %}

срок жизни таких сертификатов - сутки.

{% endnote %}

{% note warning %}

`legacy` ключ не может быть получен таким образом, ибо в этом нет никакого смысла.

{% endnote %}

### socket/pipe already exist {#socket-used}
Skotty не может запуститься, если один из сокетов/пайпов, которые он желает слушать уже заняты. Решение проблемы просто - необходимо завершить это приложение :)
Зачастую, это происходит на Windows, т.к. в остальных системах пути не пересекаются с другими приложениями. Например, если у вас запущен штатный SSH-Agent то ошибка в Skotty может выглядеть следующим образом:
```
listen on socket "default-win32-openssh" failed: listen socket of kind "pipe" failed: pipe already exists: \\.\pipe\openssh-ssh-agent
```

Скорее всего у вас запущена служба `OpenSSH Authentication Agent`, это легко проверить в PowerShell консоли:
```
PS C:\WINDOWS\system32> Get-Service ssh-agent

Status   Name               DisplayName
------   ----               -----------
Running  ssh-agent          OpenSSH Authentication Agent
```

Если это так, остановим её и отключим автозапуск:
```
PS C:\WINDOWS\system32> Set-Service -Name ssh-agent -StartupType manual
PS C:\WINDOWS\system32> Stop-Service -Name ssh-agent
PS C:\WINDOWS\system32> Get-Service ssh-agent

Status   Name               DisplayName
------   ----               -----------
Stopped  ssh-agent          OpenSSH Authentication Agent
```

Можно пробовать запустить Skotty еще раз.

### Не пускает на хост (`Permission denied` при подключении по SSH) {#ssh-permission-denied}
Если вас перестало пускать на хост по SSH, то для начала нужно убедиться с источником проблемы: это серверная сторона не принимает ключи или что-то не так с клиентской.
Поэтому для начала необходимо убедиться, что:
  - Вас не пускает на все хосты, а не какой-то один
  - Как минимум, все три ключа (`insecure`, `legacy` и `secure`) есть в выводе `ssh-add -l`. Например:
```
% ssh-add -l
256 SHA256:lXbrb2q5+ac7jtPNPQXsq32Fxnjum/DmIa0eR6wWuag Skotty key insecure on Yubikey (ECDSA-CERT)
2048 SHA256:/yk7apixZHfhrQY0Ll97qQbO12LB5q6r7Hdk9IEhsDA Skotty key legacy on Yubikey (RSA)
256 SHA256:njHscr9cJqvmyfiFWdJ5mNeUl6qj4trfX4skIzvLJqA Skotty key secure on Yubikey (ECDSA-CERT)
```
  - Cходить на хост с выводом отладочной информации: `ssh -vv target_host.yandex.net` и проверить, что:
    * дело доходит до аутентификации
    * клиент предлагает серверу для аутентификации все нужные ключи (строки вида `debug1: Offering public key: <Some key> ECDSA-CERT SHA256:<some_hash> agent`)
    * сервер их не принимает, без видимых ошибок, просто переходит к следующему ключу
    * на всякий, [вот так](https://paste.yandex-team.ru/9099607) выглядит успешное подключение

Если клиент не предлагает серверу ключи или их нет в выводе `ssh-add -l`, то нужно:
  1. Проверить, что нигде в сценариях запуска вашего шелла (`~/.bashrc`/`~/.bash_profile`/`~/.zshrc`/`etc`) не переопределяется ssh-агент и/или переменные окружения для него. Пример такой подмены - [скрипт](https://stackoverflow.com/a/18915067) для автозапуска ssh-агента.
  1. Посмотреть лог `~/.skotty/logs/agent.log`. Если там ничего толкового нет - собирайте отладочный бандл и заводите тикет, посмотрим вместе.

Если клиент отправляет ключи, но серверная сторона не принимает (i.e. просто переходит к следующему ключу, без каких-либо ошибок), то есть три наиболее вероятные причины:
  1. Истекло время жизни SSH-сертификатов и/или ключей нет на стаффе
  2. Хост, на который вы пытаетесь войти, не правильно менеджит authorized keys или у вас на него банально нет доступа
  3. Третья, смешная причина

Т.к. Skotty про клиентскую часть, то и помочь разобраться он может лишь с первым типом проблем. Для начала, необходимо сходить на специальный SSH-сервер `skotty.sec.yandex.net`. Он должен показать информацию о вашем подключении, например:
```
% ssh skotty.sec.yandex.net
Welcome to the Skotty Validation server.
Info about your connection:
  - Username: buglloc
  - Auth keys: 3
    * SHA256:lXbrb2q5+ac7jtPNPQXsq32Fxnjum/DmIa0eR6wWuag
      - type: ecdsa-sha2-nistp256-cert-v01@openssh.com
      - present on staff: yes
      - revoked: no
      - principals: buglloc
      - valid before: 2022-07-27T14:53
      - ca fingerprint: SHA256:9PsYUcGRMBPVEHlt5gZYXduP7fCceJ7BVnoV3NsXZsA
      - serial: 1651146797405871093
      - key id: skotty:insecure:buglloc:y15715412:651f4f52-1e07-4412-9a06-568b8f82f4f5
    * SHA256:/yk7apixZHfhrQY0Ll97qQbO12LB5q6r7Hdk9IEhsDA
      - type: ssh-rsa
      - present on staff: yes
    * SHA256:njHscr9cJqvmyfiFWdJ5mNeUl6qj4trfX4skIzvLJqA
      - type: ecdsa-sha2-nistp256-cert-v01@openssh.com
      - present on staff: yes
      - revoked: no
      - principals: buglloc
      - valid before: 2022-07-27T14:53
      - ca fingerprint: SHA256:9iugZLu67ykk8KutH/wJPudHxT4PismFrfy9ehLXOms
      - serial: 1651146797435841036
      - key id: skotty:secure:buglloc:y15715412:651f4f52-1e07-4412-9a06-568b8f82f4f5
  - Agent forwarded: yes
  - Agent support sudo: yes
  - Agent keys: 0

Have a great day! ;)
```
В его выводе необходимо обратить внимание на следующие вещи:
  1. Правильно ли определяется имя пользователя при подключении (e.g. `Username: buglloc`), это должен быть ваш логин на стаффе
  2. Все ли ключи перечислены (e.g. `Auth keys: 3`)
  3. Если ли ключи на стаффе (i.e. `present on staff: yes`)
  4. Не отозван ли сертификат (i.e. `revoked: no`)
  5. Не истек ли его срок службы (i.e. `valid before: 2022-07-27T14:53`, где `2022-07-27T14:53` - будущее)

Если на этом этапе все выглядит корректно и проблема явно не с сервеной частью, то создавайте тикет с выводом `ssh -vvv target_host.yandex.net` - будем разбираться :)

### Win32-OpenSSH перестал видеть ключи

`OpenSSH_for_Windows_8.9p1` и выше [обратно не совместимо изменили логику парсинга путей](https://github.com/PowerShell/Win32-OpenSSH/issues/1931) :(
Если вы давно настраивали Skotty и потом обновили `Win32-OpenSSH` могло отломиться. Чтобы убедиться в этом:
  1. Проверьте версию ssh: `ssh -V`
  2. Попробуйте посмотреть в verbose лог: `ssh -vvv skotty.sec.yandex.net`
  3. Если в выводе есть строки вида, то это оно:
```
debug3: unable to connect to pipe \\.\\pipe\\openssh-ssh-agent, error: 3
debug1: get_agent_identities: ssh_get_authentication_socket: No such file or directory
```

Для починки:
  1. Открываем `~/.ssh/config`
  2. Заменяем `\\.\pipe\openssh-ssh-agent` -> `//./pipe/openssh-ssh-agent`
  3. Заменяем `\\.\pipe\sudo-openssh-ssh-agent` -> `//./pipe/sudo-openssh-ssh-agent`
  4. Пробуем подключиться еще раз

### Не работает визард под Cygwin
К сожалению, Windows, будучи системой далекой от простых работяг, обладает даром плодить не совместимые штуки. С эмуляторами терминала та же история, Cygwin слишком особенный и визард может работать под ним не корректно. Попробуйте запустить `skotty` под `winpty`, например: `winpty skotty setup`

### Браузер запрашивает PIN для Yubikey
Т.к. Yubikey представляет из себя полноценную смарт-карту, браузер может пытаться использовать его для аутентификации на сайтах и т.д.
В случае с GNU/Linux, чаще всего, за это отвечает [OpenSC](https://github.com/OpenSC/OpenSC/wiki).
Убедиться, что это он проказничает можно проверив какой PKCS#11 провайдер настроен для вашего браузера:
  - в случае с Chromium:
    ```
    $ cat ~/.pki/nssdb/pkcs11.txt
    # ...
    library=/usr/lib/onepin-opensc-pkcs11.so
    name=OpenSC smartcard framework (0.21)
    ```
  - в случае с Firefox/Thunderbird:
    * идем в Settings -> Certificates -> Security Devices
    * смотрим в модули, если там есть `OpenSC smartcard framework` предоставляющий Yubikey - это наш клиент

Если этим PKCS#11 провайдером таки оказался OpenSC - можно просто исключить ваш Yubikey:
  1. Добываем имя Yubikey
      ```
      $ opensc-tool --list-readers
      # Detected readers (pcsc)
      Nr.  Card  Features  Name
      0    Yes             Yubico YubiKey FIDO+CCID 00 00
      ```
  2. Исключаем, добавив его имя в пропертю `ignored_readers` в файле `/etc/opensc.conf`. Например:
      ```
      $ cat /etc/opensc.conf
      app default {
        ignored_readers = "Yubico YubiKey FIDO+CCID 00 00";
      }
      ```

Детальнее в документации к OpenSC: [opensc.conf - configuration file for OpenSC](https://man.archlinux.org/man/community/opensc/opensc.conf.5.en)
