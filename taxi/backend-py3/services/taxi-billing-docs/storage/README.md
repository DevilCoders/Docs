# переменные используемые в работе generate-one.sh

MODE     -- вариант окружения (local/unstable/testing/stress/release)

DSTDIR   -- каталог, в который будут помещаться продукты метаболизма скрипта
            можно использовать $MODE в теле DSTDIR используя одинарые кавычки
            для предотвращения преждевременной подстановки
            (например: DSTDIR='/tmp/my-index-$MODE')
            (default: init-shards-${MODE})

NAME_TEMPLATE -- шаблон для построения имени выходного файла для скрипта.
                 в случае переопределения нужно указать ${pid} (pshard id)
                 (default: 'init-shard-${pid}.psql')

SCRIPT   -- тело скрипта, которое будет подставляться после установки
            настроечной переменной bd_vshard, содержащей схему vshard-а
            (default: '\ir ../schema/create.vshard.psql')

PSHARD_CONFIG_SCRIPT -- тело настроечного скрипта. лучше не менять.

EMBED_CONFIG -- позволяет хранить скрипты разных режимов в одном подкаталоге
                0 ::= делать общий скрипт настройки config.psql
                1 ::= встраивать настройку в каждый файл инициализации
                (default: 0)

ROLE_RO  -- read only пользователь

ROLE_SVC -- пользователь для сервиса

ROLE_ARC -- пользователь для архивации


# результат работы:
создаёт там файлы инициализации

# примеры использования:
```
./generate-one.sh
MODE=testing ./generate-one.sh
MODE=release DSTDIR=/tmp/rls ROLE_RO=foo ROLE_SVC=bar ROLE_ARC=baz ./generate-one.sh

MODE=release \
DSTDIR='add_index-AAA/${MODE}' \
NAME_TEMPLATE='init_${MODE}-${pid}.psql' \
SCRIPT='\ir ../add_index-AAA.psql' \
./generate-all.sh  # враппер для generate-one.sh

```
