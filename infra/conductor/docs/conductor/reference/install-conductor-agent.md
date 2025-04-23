# Установка {{ conductor-agent }} на Debian/Ubuntu

Чтобы установить {{ executor }} на Ubuntu/Debian, выполните следующие действия:

1. Добавьте в список источников следующие репозитории:

    ```no-highlight
    deb http://common.dist.yandex.ru/common stable/all/
    deb http://common.dist.yandex.ru/common stable/<архитектура>/
    deb http://yandex-hardy.dist.yandex.ru/yandex-lucid stable/all/
    deb http://yandex-hardy.dist.yandex.ru/yandex-lucid stable/<архитектура>/
    ```

1. Обновите списки пакетов и установите пакет `conductor-agent`:
    
    ```no-highlight
    $ sudo apt-get-update
    $ sudo apt-get install conductor-agent
    ```

Подробная информация приведена на странице [conductor-agent](https://wiki.yandex-team.ru/Conductor/Agent) в Вики.