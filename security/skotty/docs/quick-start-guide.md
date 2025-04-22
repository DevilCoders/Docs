# Быстрый старт

Если вы никогда не использовали Skotty, данный раздел поможет быстро его установить и настроить.
Если у вас еще нет Yubikey, его следует предварительно получить: [Как получить Yubikey?](https://docs.yandex-team.ru/skotty/howto-yubikey#new-yubikey)
Если же вы пользовались Yubikey для походов в контур Yandex.Cloud, этот раздел призван ответить на ваши вопросы: [How it works: Yandex.Cloud, pssh and so on](https://docs.yandex-team.ru/skotty/how-it-works-pssh)

## Системные требования
Некоторые платформы имеют особые требования:

  {% list tabs %}

  - GNU/Linux

    В GNU/Linux за работу со смарт-картами (а yubikey в нашем случае, это смарт-карта) отвечает демон pcscd, поэтому он должен быть установлен и запущен.

    Если используется Ubuntu и производные:
    ```
    $ sudo apt install libccid pcscd
    $ sudo systemctl enable pcscd.socket
    $ sudo systemctl restart pcscd.socket
    ```

    Тоже самое, но для Fedora:
    ```
    $ sudo dnf install pcsc-lite-ccid pcsc-lite
    $ sudo systemctl enable pcscd.socket
    $ sudo systemctl restart pcscd.socket
    ```

    Ну и про Арчеводов не забыли:
    ```
    $ sudo pacman -S ccid pcsclite
    $ sudo systemctl enable pcscd.socket
    $ sudo systemctl restart pcscd.socket
    ```

    Для корректной работы уведомлений у вас должен работать демон нотификаций (реализующий `org.freedesktop.Notifications`). Во всех больших DE (i.e. Gnome/KDE/LXDE/etc) он есть из коробки, а вот если вы пользуетесь минималистичными WM (e.g. xmonad/i3/bspwm/etc) может потребоваться его предварительная установка и настройка.

  - macOS

    Требуется macOS версии не ниже Mojave (10.14).

  - Windows

    Требуется Windows 10 не ниже 1803.

  - FreeBSD

    Во FreeBSD за работу со смарт-картами (а yubikey в нашем случае, это смарт-карта) отвечает демон pcscd, поэтому он должен быть установлен и запущен.
    Для этого:
      - устанавливаем `devel/libccid` (драйвера для USB смарт-карт) и `devel/pcsc-lite` (сам демон и обвязка вокруг):
      ```
      $ pkg install devel/libccid devel/pcsc-lite
      ```
      - включаем автозапуск `pcscd` и запускаем его для продолжения настройки

    Так же, для корректной работы уведомлений у вас должен работать демон нотификаций (реализующий `org.freedesktop.Notifications`) и быть запущен DBus. В большинстве случаев, и то и другое у вас и так есть, но если нет - стоит обзавестись.

  {% endlist %}

## Установка Skotty

{% list tabs %}

  - Кроссплатформенно

    Кроссплатформенный вариант установки предполагает наличие двух частей - лончер (занимается обновлением и прочим) и сам Skotty.

    Лончер можно получить двумя способами:
      - с помощью `ya`: `ya tool skotty --self-install`
      - самостоятельно [скачав](https://tools.sec.yandex-team.ru/skotty-launcher) и запустив: `./skotty-launcher --self-install` (macOS может не пропустить по безопасности, тогда потребуется разрешить выполнение в Settings -> Security & Privacy -> Allow anyway)

    Для macOS и GNU/Linux он установит себя в `/usr/local/bin/skotty` (запросит `sudo` для установки), для Windows в `~/.skotty/launcher`. Если вас это не устраивает - можно передать параметр `--self-install-dir` с кастомным путём для установки (убедитесь, что целевой путь доступен в `PATH`), например: `ya tool skotty --self-install --self-install-dir ~/bin`.

    {% note warning %}

    Под Windows не все эмуляторы терминала корректно обновляют переменные окружения при получении `WM_SETTINGCHANGE`. Например, ComEmu применит новые переменные окружения только для новых табов. Поэтому может потребоваться его перезапуск для дальнейшей настройки.

    {% endnote %}

    После установки лончера, можно получить последнюю версию Skotty:
    ```
    skotty --update
    ```

  - Ubuntu

    Если вы желаете обновлять Skotty вместе с остальными пакетами системы - вы можете установить его из репозитария Яндекса. Для этого:
      1. Добавляем репозитории Яндекса в `/etc/apt/sources.list.d/yandex.list`:
          ```
          deb http://common.dist.yandex.ru/common stable/all/
          deb http://common.dist.yandex.ru/common stable/amd64/
          ```
      2. Устанавливаем соответствующие GPG-ключи:
          ```
          sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7FCD11186050CD1A
          sudo apt update && sudo apt -y install yandex-archive-keyring
          ```
      3. Устанавливаем пакет `yandex-skotty`:
          ```
          sudo apt install yandex-skotty
          ```

  - Windows Software Center

      1. Переходим по [диплинку](softwarecenter:SoftwareID=ScopeId_1CECD617-ADE4-4E52-94FC-786E264C94C1/Application_63be95c8-2800-4c7d-9349-506116fa10a7) или открываем приложение Software Center и находим Skotty в поиске
      ![skotty_windows_start_panel_find_sc](_assets/skotty_windows_start_panel_find_sc.png)
      ![skotty_windows_sc_find_skotty](_assets/skotty_windows_sc_find_skotty.png)
      2. Нажмите на кнопку установить
      ![skotty_windows_sc_install_skotty](_assets/skotty_windows_sc_install_skotty.png)
      3. Переходим к настройке

  - macOS Self Service

      1. Переходим по [диплинку](jamfselfservice://content?entity=policy&id=598&action=view) или открываем приложение Self Service и находим Skotty в поиске
      ![skotty_mac_self_install](_assets/skotty_mac_self_install.png)
      2. Устанавливаем, нажимая Get
      ![skotty_mac_self_install_done](_assets/skotty_mac_self_install_done.png)
      3. Переходим к настройке

  - FreeBSD

    Т.к. широкой поддержки FreeBSD в Яндексе нет, лончер необходимо установить руками. Для этого:
      - скачиваем [skotty-launcher](https://tools.sec.yandex-team.ru/skotty-launcher)
      - запускаем его установку: `skotty-launcher --self-install`.

    По умолчанию, он установит себя в `/usr/local/bin/skotty` (запросит `sudo` для установки). Если вас это не устраивает - можно передать параметр `--self-install-dir` с кастомным путём для установки (убедитесь, что целевой путь доступен в `PATH`), например: `skotty-launcher --self-install --self-install-dir ~/bin`.

{% endlist %}

## Настройка

После того как Skotty был установлен - самое время настроить его для работы с yubikey.
Для этого:
  1. запускаем настройку: `skotty setup`
  2. проходим визард
  3. на этом настройка Skotty закончена и стоит перейти к [настройке SSH клиента](https://docs.yandex-team.ru/skotty/ssh-client)

Если `skotty setup` не видит Yubikey (i.e. выдает ошибку `no keyring available`), можно обратиться к разделу [Skotty не видит Yubikey](https://docs.yandex-team.ru/skotty/troubleshooting#no-keyring-available) за диагностикой и починкой.

{% note warning %}

Если Yubikey ранее уже использовался (например, если вы работали в Яндекс.Облаке), Skotty попросит ввести корректный `PIN`. В противном случае, предложит сбросить Yubikey (очищаются все слоты, генерится новый PIN/PUK/Management key). В этом случае вы можете как сгенерировать новый `PIN`/`PUK`, так и ввести желаемые.

{% endnote %}

Например:
[![пример настройки](_assets/skotty_setup.png)](https://jing.yandex-team.ru/files/buglloc/skotty_setup.png?1)


{% note warning %}

Все ранее выписанные сертификаты в Skotty для этого токена (будь то yubikey или софтварное хранилище) будут отозваны. Если вы хотите только обновить сертификаты не настраивая заново токен - воспользуйтесь `skotty renew`, он обновит сертификаты и не будет отзывать лишнего.

{% endnote %}
