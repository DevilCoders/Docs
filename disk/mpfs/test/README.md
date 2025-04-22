## Инфраструктура тестирования MPFS

Данное руководство содержит необходимую информацию для того, чтобы быстро начать писать тесты для MPFS.

### Как запускать тесты
#### Настройка окружения
0. Устанавливаем run-time зависимости от .deb пакетов:

   ```sh
   sudo apt-get install yandex-environment-development \
                     verstka-disk-emails \
                     python-mpfs-disk \
                     python-mpfs-api \
                     python-ylog \
                     libauth-client-parser-python
   ```

0. Устанавливаем зависимости от python модулей:

    ```sh
    sudo pip install -r test-requirements.txt
    ```

0. Правим права для логов:

    ```sh
    sudo chmod 777 /var/log/mpfs
    # Для админки доступов
    sudo chmod -R 777 /var/log/mpfs-api-admin
    ```

0. Настраиваем mongodb для тестов:

  0. Устанавливаем версию `2.6.*`:

    ```sh
    sudo apt-get install 'mongodb=1:2.6.*'
    ```

  0. Делаем рамдиск для монги:

    ```sh
    sudo mkdir /ramdata
    sudo chown mongodb:mongodb /ramdata
    sudo mount -t tmpfs -o size=24000M tmpfs /ramdata
    ```

  0. Конфигурируем (конфиг по умолчанию: `/etc/mongodb-default.conf`):

    ```txt
    nojournal = true
    smallfiles=true
    dbpath=/ramdata
    ```

  0. Перезапускаем сервис:

    ```sh
    sudo service mongodb restart
    ```

#### Запуск тестов
0. Запустить тесты в обычном режиме:

    ```sh
    cd test
    py.test -vs parallelly/api
    ```

0. Запустить тесты параллельно:

    ```sh
    py.test -n 8 parallelly/api
    ```

0. Запустить отдельный тест из suite'a:

    ```sh
    py.test -vs parallelly/api/disk/trash.py::TrashTestCase::test_restore
    ```

0. Запустить тесты против реального инстанса MongoDB:

   ```sh
   MPFS_REAL_MONGO=TRUE ./tools/pytest.sh -v test/parallelly/api/disk/trash.py
   ```

0. Запустить тесты Админки Доступов:

   ```sh
   cd test/api_admin
   py.test [api_auth | api_auth/test_validators.py]
   ```

### Типы тестов: unit/integration/system

Тесты MPFS разделены на три типа:

* юнит тесты
* интеграционные тесты
* системные тесты

Юнит тесты направлены на тестирование отдельных кусочков внутренних компонент MPFS: тестирование внутренней логики. Обычно эти тесты проверяют отдельный метод, где содержится логика, отвечающая за отдельную задачу.

Интеграционные тесты направлены на тестирование взаимодействия внутренних компонент MPFS и связей внутри одной компоненты. Среди них обособлены тесты взаимодействия с внешней компонентой (DB, Search и прочее), которую не замещаем заглушкой.

Системные тесты - это набор тестов, которые запускаются против live кластера MPFS. В этих тестах проверяются сложные пользовательские сценарии, валидация API. Такие тесты представлены java тестами и расположены в отдельном репозитории: [autotests/disk/cloud-api](https://github.yandex-team.ru/testpers/disk-cloud).

Тесты представленные в данном репозитории имеют следующую структуру:

    ```
    test/
    ├── api_admin # тесты для Админки Доступов
    ├── component # интеграционные
    ├── consistently # интеграционные
    ├── fixtures 
    ├── helpers
    ├── parallelly # интеграционные
    └── unit
    ```

### Общие рекомендации

* Действия по подготовке окружения тестов стоит выносить в [setup_method/teardown_method](http://pytest.org/latest/xunit_setup.html#method-and-function-level-setup-teardown).

* Базовый класс тестов стоит импортировать до любых импортов из пакета `mpfs`, т.к. в некоторых модулях `mpfs` исполняется код при импорте, и нужно подготовить окружение для этого кода.
