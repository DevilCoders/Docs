# Intro

Skotty - кастомный SSH agent для работы с Яндексовым SSH PKI поверх Yubikey, который:
  - умеет делать первичную настройку [Yubikey](https://docs.yandex-team.ru/skotty/howto-yubikey)
  - может получить и обновить ваши SSH сертификаты
  - хранит приватную часть ключа в разнообразных хранилищах:
    * yubikey (предпочтительный вариант)
    * файличках
    * хранилище ключей вашей OS:
      - macOS - Keychain
      - GNU/Linux - Secret Service
  - предоставляет к ним доступ по ssh agent протоколу поверх:
    * UNIX-socket (GNU/Linux && macOS && Windows):
      - используется и поддерживается подавляющим большинством SSH клиентов под GNU/Linux и macOS
      - работает в WSL под Windows
    * Named pipes (Windows):
      - использует Win32-OpenSSH
      - использует Putty (версии 0.74 и выше)
    * Pageant (Windows):
      - использует Putty и множество кастомных клиентов (Far NetBox, JetBrains, etc)
    * Cygwin UNIX Socket (Windows)
  - может строить many-to-many комбинации из сокетов и хранящихся в них ключей
  - реализовывает кастомный экстеншен для поддержки LDAP-less аутентификации в `sudo`
  - любит вас :3

Помимо прочего, существует:
  - UI в котором можно посмотреть записанные на вас токены: [https://skotty.sec.yandex-team.ru/](https://skotty.sec.yandex-team.ru/)
  - Чатик сочувствующих: [Oh My Yubikey (Skotty public chat)](https://t.me/+ga7UEj4gQ4JkZWUy)