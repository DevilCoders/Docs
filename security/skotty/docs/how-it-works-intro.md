# How it works: в общих чертах

Концептуально, Skotty можно разделить на несколько частей:
  - генерация, аттестация и энролл SSH-сертификатов
  - представление себя в качестве SSH-агента
  - взаимодействие с sudo

## Генерация, аттестация и энролл SSH-сертификатов

Для того чтобы покрывать все наши нужды и по дороге ничего не сломать Skotty генерирует 5 ключей:
  - `renew` - ECDSA с [touch policy](https://docs.yandex-team.ru/skotty/why#touch-policy) "never". Этот ключ не доступен ни в одном из сокетов и используется только для полуавтоматического обновления сертификатов в yubikey
  - `secure` - ECDSA с [touch policy](https://docs.yandex-team.ru/skotty/why#touch-policy) "cached". Должен использоваться для походов по SSH в продакшн
  - `insecure` - ECDSA с [touch policy](https://docs.yandex-team.ru/skotty/why#touch-policy) "never". Должен использоваться для походов по SSH во все другие окружения
  - `sudo` - ECDSA с [touch policy](https://docs.yandex-team.ru/skotty/why#touch-policy) "always". Используется для аутентификации в `sudo`
  - `legacy` - RSA с [touch policy](https://docs.yandex-team.ru/skotty/why#touch-policy) "never". Это старый добрый, обычный RSA ключик, который пригодится для похода в legacy системы и на период миграции

После генерации Skotty:
  1. [аттестует](https://docs.yandex-team.ru/skotty/why#attestaciya) каждый сертификат
  2. отправляет запрос в энролл-сервис, получает авторизационный токен и авторизационный линк (по нему вы перехолили на этапе первоначальной настройки)
  3. поллит выдачу сертификатов

В это время энролл сервис:
   1. проверяет запрос (e.g. что все нужные политики выставлены)
   2. авторизует пользователя с помощью одноразовой ссылки и в случае успеха
   3. в случае успеха - генерирует и подписывает на нужных CA публичный ключки
   4. возвращает их skotty в обмен на авторизационный токен

Подробнее о процессе энроллмента читайте в разделе [энролл и обновление сертификатов](https://docs.yandex-team.ru/skotty/how-it-works-enroll).

На этом основная часть по настройке окончена и Skotty может выполнять свои функции.

{% note warning %}

SSH-сертификаты имеют срок жизни и их нужно периодически (в зависимости от хранилища) обновлять.

{% endnote %}

## Представление себя в качестве SSH-агента

Чаще всего переход на аутентификацию по SSH-сертификатам предполагает замену SSH-клиента на кастомный. В нашем случае, это был совсем не вариант и мы выбрали путь реализации SSH-агента т.к. нам было важно:
  - ничего не сломать (например, IDE от JetBrains самостоятельно реализует клиента и подсунуть ей собственный не возможно). Все что умеет взаимодействовать с SSH-агентов (а это почти любая приложенька, которой нужен поход по SSH) должно продолжить работать как и раньше
  - не менять ваши привычки. Нравится использовать Putty? - пожалуйста. Предпочитаете ходить из под WSL - ваше право

Таким образом Skotty умеет предоставлять произвольное количество сокетов, которые содержат произвольный набор ключей. В т.ч. вас никто не ограничивает в добавлении собственных ключей (e.g. `ssh-add ~/.ssh/my_cool_key`), превращая Skotty в полноценный SSH-агент.

К примеру, в конфигурации вида:
```
# ~/.skotty/config.yaml

sockets:
- default: true
  kind: unix
  name: default
  path: /home/buglloc/.skotty/sock/default.sock
  keys:
  - secure
  - insecure
  - sudo
  - legacy
- default: false
  kind: unix
  name: insecure
  path: /home/buglloc/.skotty/sock/insecure.sock
  keys:
  - insecure
  - sudo
  - legacy
- default: false
  kind: unix
  name: sudo
  path: /home/buglloc/.skotty/sock/sudo.sock
  keys:
  - sudo
```

Skotty будет слушать три UNIX-сокета:
  - `/home/buglloc/.skotty/sock/default.sock` - предоставляет доступ ко всем ключам
  - `/home/buglloc/.skotty/sock/insecure.sock` - так же как и `default`, но без `secure` ключа
  - `/home/buglloc/.skotty/sock/sudo.sock` - только ключ для взаимодействия с `sudo`

Демо:
```
$ SSH_AUTH_SOCK=/home/buglloc/.skotty/sock/default.sock ssh-add -l                                       
2048 SHA256:XQYYJNfqlGlTc5yeVlJ+5Bngilw97oWFQR12/gqmFOc legacy on Yubikey (RSA)
256 SHA256:aInTNsVSq7ujixYAJ8F1cQajEwfoHNTnPNe/gCw/enk insecure on Yubikey (ECDSA-CERT)
256 SHA256:mqysdH/zAcC1sigOfexhHhyl9vl9CANOJAaIy/QToaY secure on Yubikey (ECDSA-CERT)

$ SSH_AUTH_SOCK=/home/buglloc/.skotty/sock/insecure.sock ssh-add -l
2048 SHA256:XQYYJNfqlGlTc5yeVlJ+5Bngilw97oWFQR12/gqmFOc legacy on Yubikey (RSA)
256 SHA256:aInTNsVSq7ujixYAJ8F1cQajEwfoHNTnPNe/gCw/enk insecure on Yubikey (ECDSA-CERT)

$ SSH_AUTH_SOCK=/home/buglloc/.skotty/sock/sudo.sock ssh-add -l
The agent has no identities.
```
(`sudo` ключ отсутствиет в выдаче, т.к. им нельзя аутентифицироваться по SSH)

## Взаимодействие с sudo

Аутентификация в sudo работает благодаря двум вещам:
  1. Для sudo в PAM настроен кастомный модуль [pam_skotty_sudo.so](https://a.yandex-team.ru/arc/trunk/arcadia/security/skotty/pam_skotty_sudo)
  2. Skotty реализует кастомный эктеншен `skotty-sudo`

Таким образом, когда для вас настроено "парольное" sudo происходит следующее:
  1. sudo дергает PAM
  2. PAM дергает `pam_skotty_sudo.so`
  3. `pam_skotty_sudo.so` идет в UNIX-сокет (`env[SSH_AUTH_SOCK]`) с просьбой подписать рандом
  4. Если вы сфорваридили сокет Skotty при подключении по SSH, то он получит запрос, подпишет рандом и отправит ответ `pam_skotty_sudo.so`
  5. `pam_skotty_sudo.so` получив ответ, проверяет подпись рандома (дабы убедиться, что именно вы подписали рандом на правильном ключе), сам рандом и если все сошлось - разрешает доступ

{% note warning %}

При использовании tmux/screen/etc вы должны позабодиться о пробросе живого сокета.

{% endnote %}
