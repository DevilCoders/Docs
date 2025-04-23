### mysql-direct-yt-sync

ОЧЕНЬ ВАЖНО!!!!!!!
При изменении схемы данных нужно в файлах
https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/mysql-direct-yt-sync/etc/direct/binlog-to-yt-sync/sync-path.version
https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/mysql-direct-yt-sync/src/main/resources/app-production.conf?rev=5272215#L99
изменить версию на +1

Приложение-синхронизатор, переливающее данные и бинлоги из MySQL в динамические таблицы YT.
Может работать в двух режимах:
1. Начальный импорт
2. Доливка данных из бинлогов

Начальный импорт всех таблиц может занимать до 2 суток (в проде обычно в два раза быстрее, чем на девтестах).

Здесь есть некоторое описание того, что происходит: https://wiki.yandex-team.ru/users/buhter/gridsreleasesanddevelopment/

Также есть переключатель
1. Синхронизировать таблички для нового интерфейса (опция включена по умолчанию на кластерах `ZENO` и `SENECA-XXX`)
2. Синхронизировать все таблички MySQL как есть (опция включена по умолчанию на кластерах `HAHN` и `ARNOLD`)

#### Как запустить локально

Для локального запуска необходимо выполнить следующие приготовления:

1. Определиться с местом в Yt, куда будут заливаться данные

    По умолчанию для девтеста это `//home/direct/test/mysql-sync/devtest/` на кластере `ZENO`.
    Но мы ведь не хотим затереть все данные на девтесте? Поэтому лучше выбрать другое место где-нибудь в сторонке.
    Возьмём к примеру `//home/direct/tmp/elwood/mysql-sync3/`.
    В конфиге `app-devtest.conf` (и `app-development.conf` тоже, если вы планируете запускать с опцией `-Dyandex.environment.type=DEVELOPMENT`)
    нужно указать

    ```
    yt-sync.path.root: "//home/direct/tmp/elwood/mysql-sync3/"
    ```

    Ещё способ: вместо этого изменить `yt-sync.path.version` на "v.elwood", к примеру.
    Всё будет заливаться в эту поддиректорию.

2. Определиться с количеством обрабатываемых шардов

    По умолчанию синхронизатор будет обрабатывать все шарды. Если для первоначального тестирования
    это не нужно, можно закомментировать лишние в том же конфиге:

    ```

        dbnames: [
            "ppc:1"
            "ppc:2"
            //"ppc:3"
            //"ppc:4"
            //"ppc:5"
            //"ppc:6"
            //"ppc:7"
            //"ppc:8"
            //"ppc:9"
            //"ppc:10"
            //"ppc:11"
            //"ppc:12"
            //"ppc:13"
            //"ppc:14"
            //"ppc:15"
        ]
    ```

    Синхронизатор будет работать не в пример быстрее.

3. Установить mysqld (для запуска в режиме доливки из бинлогов)

    Работает с версией mysql 5.7.18 (проверенно). С 8'ой на mac не работает.
    скачать можно здесь: https://downloads.mysql.com/archives/community
    Затем добавить path:
    echo 'export PATH="/usr/local/mysql-5.7.18-macos10.12-x86_64/bin:$PATH"' >> ~/.bash_profile

    Возможно, ещё придётся подправить метод `ru.yandex.direct.mysql.MySQLServerBuilder.getServerVersion()`,
    который не всегда может распарсить версию mysql из названия пакета. Например, так:

    ```
    public Version getServerVersion() throws InterruptedException {
        String output = Processes.checkOutput(this.copy().addExtraArgs("--version").createProcessBuilder());
        Matcher matcher = Pattern.compile("\\sVer\\s+(.+?)\\s").matcher(output);
        if (!matcher.find()) {
            throw new IllegalStateException("Can't parse version: " + output);
        } else {
            return Version.valueOf("5.7.22");  //matcher.group(1));
        }
    }
    ```

4. Закомментировать ненужные таблицы или ограничить данные.

    Часто для отладки новых таблиц достаточно прогнать только их импорт. Для этого нужно
    закомментировать ненужные Task-классы в проекте. Они лежат в
    `mysql-direct-yt-sync/src/main/java/ru/yandex/direct/mysql/ytsync/task/instances`

    Либо можно ограничить импортируемые из таблиц данные, добавив опцию `-Dyt-sync.import.chunks-limit=1`

5. Указать случайное число в качестве номера слейва (для запуска в режиме доливки из бинлогов)

    Это нужно для того, чтобы слейвы не конфликтовали. Если этого не сделать, то свежезапущенный
    "слейв" будет мешать уже работающим инстансам синхронизатора, и наоборот. В результате этого
    слейвы будут регулярно отключаться и переподключаться только через 15 секунд.

    ```
    mysql-server-id: 46929

    zeno {
        use-slaves = false
    }
    ```

6. Запустить `RunInitialImport` или `ProcessBinlogFromServer`

    В зависимости от того, в каком режиме требуется запуск.
    `ProcessBinlogFromServer` тоже умеет запускать начальный импорт, если указана соответствующая опция.
