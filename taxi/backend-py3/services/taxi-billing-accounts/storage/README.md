# переменные используемые в работе generate.sh

MODE     -- вариант окружения (local/unstable/testing/stress/release)

DSTDIR   -- каталог, в который будут помещаться продукты метаболизма скрипта
            (default: init-shards-${MODE} в том же каталоге, что и generate.sh)

ROLE_RO  -- read only пользователь

ROLE_SVC -- пользователь для сервиса

ROLE_ARC -- пользователь для архивации


# результат работы:
скрипт копирует общие файлы из common/ в каталог $DSTDIR
или в init-shards-${MODE} и создаёт там же файлы инициализации

# примеры использования:
```
./generate.sh
MODE=testing ./generate.sh
MODE=release DSTDIR=/tmp/rls ROLE_RO=foo ROLE_SVC=bar ROLE_ARC=baz ./generate.sh
```
