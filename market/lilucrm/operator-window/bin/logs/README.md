### Установка
Чтобы переместить скрипты на сервера логов (в папку ~/bin, которая обычно есть в PATH)
и сгенерировать там списки сервисов, запустите ``install-to-logview.sh``.

Списки сервисов будут расположены в ~/services и генерируются на основании набора папок, лежащих в /mnt/nanny,
так что, если они никогда не монтировались на сервере логов (или он был переналит),
то может потребоваться сначала примонтировать их вручную или скопировать ~/services с другого сервера логов.

### Работа
Смонтировать логи в нужном окружении можно скриптом ``ow-testing.mount-logs``,
а получить список файлов логов - ``ow-testing.list-logs``.

**Usage:**: ``ow-testing.list-logs [log-file-name [directory]]``
* `log-file-name` - Имя файла с логами. По умолчанию: `market-operator-window.log`
* `directory` - директоря, в которой ищем логи внутри папки сервиса. По умолчанию: `operator-window`

Например:
```sh
local$ ssh logview.market.yandex.net
$ ow-testing.mount-logs
Service 'testing_market_operator_window_sas' on server 'sas2-1268.search.yandex.net' already mounted
Service 'testing_market_operator_window_vla' on server 'vla1-4584.search.yandex.net' already mounted
$ ow-testing.list-logs
/mnt/nanny/testing_market_operator_window_sas/13050@sas2-1268.search.yandex.net/operator-window/market-operator-window.log
/mnt/nanny/testing_market_operator_window_vla/18429@vla1-4584.search.yandex.net/operator-window/market-operator-window.log
$ ow-testing.list-logs market-operator-window-access-tskv.log | xargs fgrep "$PATTERN"
$ ow-testing.list-logs lilucrm-operator-window-access-tskv.log nginx | xargs fgrep anton0xf | head -n1
/mnt/nanny/testing_market_operator_window_sas/13050@sas2-1268.search.yandex.net/operator-window/../nginx/lilucrm-operator-window-access-tskv.log:tskv     tskv_format=tskv-market-default timestamp=2018-01-25T00:23:56   ....

# remount logs
$ ow-testing.remount-logs
```
**UPD:** теперь поддерживаются глобы (синтаксис соответствует опции `-name` команды `find`)
Пример поиска в уже сжатых логах по дате (с сортировкой по времени):
```sh
$ ow-production.list-logs 'market-operator-window.log.2019-10-10.*' | xargs zgrep 'uploadB2bTkCallsToMdsThread.*FileImporter' | sort -k2 -t:
```

**UPD 2020-02-24:** добавлено несколько хэлперов с префиксом `log_`.

Для работы со входом вида `file_name:log_line`:
* `log_sort` - сортирует свой вход, гнорируя часть до точки с запятой. Дополнителные параметры передаёт в `sort`
* `log_file-to-host` - если левая часть имеет вид `/mnt/nanny/*/$dc-$host-*`, то укаорачивает её до `$dc-$host`. Дополнителные параметры передаёт в `sed`

Для работы с логом, как с набором многострочных записей
* `log_zero-sep` - за счёт чего всё работает - разделяет записи нулевым байтом. если переданы имена файлов, то приписывает из в начало каждой записи, как это делает grep, или (что то же самое) как описано выше
* `log_rm-zero-sep` - удаляет нулевые байты из потока
* `log_zero-tail` - замена для `tail -z`, которая не работает на logview
А дальше можно пользоваться любыми утилитами, понимающими zero terminated вход: `grep -z`, `sed -z` и пр.

Например, так можно получить последние два стектрейса от упавших сегодня фоновых задач
(с указанием хоста, на котором был запуск):
```sh
$ ow-testing.list-logs | xargs log_zero-sep | fgrep -az crushed | log_file-to-host -z | log_sort -z \
    | log_zero-tail 2 | log_rm-zero-sep
```

```
sas2-1268:[2020-01-24 17:05:00,103] ERROR [pool-15-thread-6] reqID=1579874700000/832d0323ad2a1d4d6d39ecdfec6e3152 r.y.m.c.o.s.s.ScheduledTaskExecutor: Task smartcallsCheck crushed
java.lang.RuntimeException: org.postgresql.util.PSQLException: The column name updated was not found in this ResultSet.
        at ru.yandex.market.jmf.db.util.DbHelpers.getOffsetDateTime(DbHelpers.java:72)
...
```

**UPD 2020-08-18:** Ускорил сниппет выше с помощью пралаллельного запуска на всех логах и оформил в отдельный
вспомогательный скрипт `log_search`. Пример:

```sh
$ ow-production.list-logs | log_search -F '1597740884086/a258c0a7e4d52b40b59659a71a01a025'
```

**UPD 2021-04-16:** Теперь скрипт `log_search` можно использовать и с архивированными логами:

```shell
$ ow-production.list-logs 'market-operator-window.log.2019-10-10.*' | log_search -F '1597740884086/a258c0a7e4d52b40b59659a71a01a025'
```