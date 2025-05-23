# Как собрать tmpfs том в инстансе

## Требования {#reqs}

Для включения tmpfs в инстансе необходимо, чтобы он был:

1. [Изолированным по файловой системе](https://wiki.yandex-team.ru/runtime-cloud/nanny/howtos/move-to-rootfs/)

## Ограничения {#constraints}

1. tmpfs-вольюм необходимо заводить за пределами рабочей директории инстанса, например, в корне, e.g. `/tmpfs`. 

2. Размер tmpfs всегда ограничен. Он должен быть **строго меньше объема памяти инстанса (лимита)**. Должен быть также зазор между лимитом и tmpfs, который должен быть достаточен для потребляемой памяти приложения и нужного объема page cache (нужен для записи логов и для чтения файлов). **Если этого не учесть, приложение ждет риск словить OOM**.

3. Файлы tmpfs не исчезают при падении самого приложения - соответственно, память контейнер продолжит потреблять. Если спровоцируется ООМ по сценарию из п.2, то **приложение может больше не подняться** из-за нехватки памяти по сценарию "циклического ООМ". **Очищайте данные в tmpfs при остановки контейнера**.

## Инструкция {#how-to}

1. Установить в образ инстанса `portoctl` (или porto API при использовании python-скриптов). Для этого достаточно в интерфейсе Nanny выбрать OS-версию слоя файловой системы:

    ![img](https://jing.yandex-team.ru/files/sshipkov/Screenshot%20from%202019-12-23%2018-58-57.4ca5952.png)

1. Перед стартом приложения выполнить следующий скрипт:

    ```
    if [ ! -e /tmpfs ]; then
        portoctl vcreate /tmpfs backend=tmpfs space_limit=1Gb
    fi
    ```

{% note warning %}

**Указывать space_limit необходимо обязательно**, значение должно быть строго меньше чем квота инстанса по памяти.

{% endnote %}
