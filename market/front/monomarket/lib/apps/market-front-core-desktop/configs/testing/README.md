Конфигурация testing окружения Маркета
-----------------------------

#### Переменные окружения, с группировкой по конфигам:

  + `luster.conf.js`
    - `LOGS_DIR` Папка, в которую luster будет складывать stdout, stderr приложения. **Необходима для запуска**

  + `node.js`
    - `MEMCACHED_SERVERS` Переменная вида `<addr>:<port>` для соединения с memcached. Пробрасывается из [конфига сборки](https://github.yandex-team.ru/market/packages/blob/aa14a7dcd0de6eba4f759231368476093e7e0f3d/yandex-market-frontend/PKGBUILD#L168)(файл мог обновиться). **Необходима для запуска**
    - `SKIP_TVM` Пропустить инициализацию TVM. Требуется для корректного импорта роутов в автотестах.

  + `stout.js`
    - `NODE_PORT` Номер tcp порта(или путь на файловой системе для UNIX Socket) где будет ожидать соединения наше приложение. **Необходима для запуска**
    *В этом окружении используются именно UNIX Socket'ы, за подробностями можно сходить в [конфиг сборки](https://github.yandex-team.ru/market/packages/blob/aa14a7dcd0de6eba4f759231368476093e7e0f3d/yandex-market-frontend/PKGBUILD#L159)(файл мог обновиться)*

#### Borschik

Обратите внимание на вставку `<_staticpub>` внутри borschik конфига для этого окружения(и всех остальных, кроме development). Эта штука будет заменена на этапе сборки переменной из [конфига сборки](https://github.yandex-team.ru/market/packages/blob/aa14a7dcd0de6eba4f759231368476093e7e0f3d/yandex-market-frontend/PKGBUILD#L178)(файл мог обновиться).
