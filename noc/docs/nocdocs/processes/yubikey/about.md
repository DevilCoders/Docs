# Yubikey на страже NOC

В этой статье расскажем про то как правильно получить и настроить yubikey.

Автор: [Вадим Воловик](https://staff.yandex-team.ru/vdvolovik)



Эта статься является дополнением статьи ИБ про yubikey. Она разработана специально для сотрудников Отдела офисной инфраструктуры, чтобы пояснить специфичные вопросы для NOC.

Оригинал доступен по ссылке [https://docs.yandex-team.ru/skotty/quick-start-guide](https://docs.yandex-team.ru/skotty/quick-start-guide)

{% note tip %}

Если у вас что-то не получается, не работает, отвалился доступ и пр., то пишите в чат [Доступы NOC](https://t.me/+5u_T54DBR_43ZTZi)

{% endnote %}

## Что такое yubikey

Yubikey - это специальных токен для безопасного хранения ваших приватных ключей. Выглядят они как флешки и вставляются в USB A/C.

![](./_images/img1.png)

## Где его получить

Можно получить в офисе в:
- вендомате
- у хелпов

Если вы находитесь в другом городе и не можете получить доступ к офису, то можно заказать yubikey через специальную форму: [https://help.yandex-team.ru/?form=498&search=&skip_service_card=true](https://help.yandex-team.ru/?form=498&search=&skip_service_card=true). 

Также можно через Helpdesk. Алгоритм следующий:
- Переходим на страницу [Helpdesk](https://help.yandex-team.ru/?search=)
- Оборудование -> [VPN-токен](https://help.yandex-team.ru/?form=rutoken)
- Заполняем форму:
  - указываем адрес доставки: `Другой` и пишем свой адрес
  - ЦФО: `ITMS41`
  - Номер сервиса: `SE928`
- После заведения формы, переходим в тикет и пишем в комментарии, что требуется именно yubikey. Например, так:
```
Прошу доставить yubikey для разъема USB A (или USB C)
```
- Ожидайте

## Что делать после получения yubikey

{% note warning %}

Не запускайте настройку `skotty` из под `sudo` или `root`

{% endnote %}

- Достаньте yubikey из упаковки
- Вставьте yubikey в устройство
- Выполните [подготовительные](https://docs.yandex-team.ru/skotty/quick-start-guide#sistemnye-trebovaniya) действия 
- Установите [Skotty](https://docs.yandex-team.ru/skotty/quick-start-guide#ustanovka-skotty)
- Пройдите настройку Skotty:
  - запускаем настройку `skotty setup`. Не запускайте настройку `skotty` из под `sudo` или `root`
  - сохраняем PIN и PUK где-то в безопасном месте
  - переходим по ссылке, которая генерируется. Ищите ключевое слово `URL`
  - пройдите проверку
  - получите ключи:
    - legacy
    - insecure
    - secure
- Добавьте на стафф ключи:
  - yub-legacy
  - yub-insecure
  - yub-secure
- настройте `~/.ssh/config`
  ```
  Host bb.yandex-team.ru
  PubkeyAcceptedKeyTypes +ssh-rsa
  IdentityAgent ~/.skotty/sock/default.sock

  Host *.yandex.net
  # Forward only "sudo" socket to the untrusted environment
  ForwardAgent /Users/vdvolovik/.skotty/sock/sudo.sock
  # But authenticate through default socket
  IdentityAgent /Users/vdvolovik/.skotty/sock/default.sock

  Host *.yndx.net
  # Forward only "default" socket to the untrusted environment
  ForwardAgent /Users/vdvolovik/.skotty/sock/default.sock
  ```
- после этого у вас прорастет доступ с yub-ключами
- переместите ваш текущий id_rsa: 
  ```
  mkdir ~/.ssh/bak
  mv ~/.ssh/id_rsa* ~/.ssh/bak
  ```
- произведите замену штатного ssh-агента по [инструкции](https://docs.yandex-team.ru/skotty/ssh-client#zamena-shtatnogo-ssh-agenta)
- проверьте доступ

Дополнительно, если вам нужно ходить на сетевое железо или `noc-myt`, `noc-sas`, то тогда вам еще надо заменить ключ в cvs. Для этого пишите [Воловику Вадиму](https://staff.yandex-team.ru/vdvolovik), он произведет замену. После раскатки кронами вашего ключа, надо проверить доступ.

## Тонкая настройка Yubikey

### Для Yandex.Cloud

Чтобы ходить на устройства Yandex.Cloud не под агентом skotty, то в конфигурацию ssh необходимо добавить следующие строки:
```
Host abcd
  ForwardAgent /var/folders/wy/7l90n3592vbd72ssr4m92lf5lryd42/T//ssh-5Fz4uSgVxOJ5/agent.25769
```
