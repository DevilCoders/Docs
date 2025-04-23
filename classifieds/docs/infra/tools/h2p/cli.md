# Command line interface

## Установка {#install}
Актуальная версия `1.14`

{% list tabs %}

- macOS

  ```shell
  brew tap YandexClassifieds/vertis ssh://git@bb.yandex-team.ru/yandex-classifieds/homebrew-vertis.git
  brew update
  brew install h2p
  ```

- linux

  ```shell
  sudo curl https://proxy.sandbox.yandex-team.ru/3282150423 -o /usr/local/bin/h2p && sudo chmod +x /usr/local/bin/h2p
  ```

- windows

  {% note warning %}

  Чтобы заработало на Winodows, необходимо запускать под WSL2.

  [Подробнее](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

  {% endnote %}

  ```shell
  sudo curl https://proxy.sandbox.yandex-team.ru/3282150423 -o /usr/local/bin/h2p && sudo chmod +x /usr/local/bin/h2p
  ```

{% endlist %}

## Важные особенности
* Для корректной работы необходим запущенный `ssh-agent`
* Для работы с MySQL потребуется консольный клиент `mysql`
* Для работы с PostgreSQL потрубется консольный клиент `psql`
* Если у вас логин на Стаффе не совпадает с именем в системе, `h2p` не будет корректно работать. Необходимо определить переменную окружения `H2P_USER` - в ней должен лежать ваш логин на Стаффе

  {% cut "Пример" %}

  `export H2P_USER=opyakin-roman`

  {% endcut %}
* При указании ключика `-t` вы открываете туннель в **тестинг**, а не прод. В тестинг никаких ролей **запрашивать не нужно** - у всех есть доступ всюду

## Опции
* `-d, --datacenter` Позволяет указать конкретный датацентр.
Если указанный датацентр недоступен (например, во время учений), то запросы работать не будут
* `-t, --test` При указании опции запросы будут идти в **тестинг**, а не прод
* `-w, --write` Включает возможность записи в базы данных
* `-s, --skip-validate` Отключает валидацию на стороне клиента (на сервере остается - то есть **не получится сходить в сервис без роли**). При указании опции не проверяет: наличие роли в IDM, окружение прод/тест. Может быть полезно для автоматизации
* `-v, --verbose` Включает дополнительное логирование


## Примеры {#examples}
{% list tabs %}

- Сервис

  * Открыть туннель до провайдс `http` сервиса `general-www` на локальном 8080 порту:

    `h2p general-www-http 8080`

  * Открыть туннель до провайдс `http` сервиса `general-www` в датацентре **sas**:

    `h2p general-www-http -d sas`

  * Открыть туннель до провайдс `http` сервиса `general-www` в бранче `BRANCH-1`:

    `h2p general-www-BRANCH-1-http`

  * Открыть туннель до конкретного аллокейшена провайдс `monitoring` сервиса `general-www`:

    `h2p general-www-monitoring@allocid=05ff25b4-2a01-eb5a-0329-11c0c5e6e043`

  * Открыть туннель до провайдс `http` сервиса `general-www` в **тестинге**:

    `h2p general-www-http -t`

  * Сделать `curl` запрос до провайдс `http` сервиса `general-www` через h2p:

    `h2p general-www-http '/do-stuff?param=value&p2=v2 -X POST'`

- MySQL

  * Открыть туннель до базы `rabota_stats` в кластере `mdb14lu9g7t0rhf166t8` **в режиме только чтение**:

    `h2p mysql-mdb14lu9g7t0rhf166t8@rabota_stats`

  * Открыть туннель до базы `rabota_stats` в кластере `mdb14lu9g7t0rhf166t8` **с возможностью записи**:

    `h2p mysql-mdb14lu9g7t0rhf166t8@rabota_stats -w`

  * Открыть туннель до базы `rabota_stats` в кластере `mdbhcrb5ilrspua8n2qm` в **тестинге**:

    `h2p mysql-mdbhcrb5ilrspua8n2qm@rabota_stats -t`

  * Сделать SQL запрос к базе `rabota_stats` в кластере `mdb14lu9g7t0rhf166t8` **в режиме только чтение**:

    `h2p mysql-mdb14lu9g7t0rhf166t8@rabota_stats 'SELECT 1;'`

  * Сделать SQL запрос к базе `rabota_stats` в кластере `mdb14lu9g7t0rhf166t8` **с возможностью записи**:

    `h2p mysql-mdb14lu9g7t0rhf166t8@rabota_stats 'UPDATE users SET column1 = 1 WHERE column2 = 2;'`

- PostgreSQL

  * Открыть туннель до базы `db1` в кластере `mdba7mivql6v0aee7uev` **в режиме только чтение**:

    `h2p pg-mdba7mivql6v0aee7uev@db1`

  * Открыть туннель до базы `db1` в кластере `mdba7mivql6v0aee7uev` **с возможностью записи**:

    `h2p pg-mdba7mivql6v0aee7uev@db1 -w`

  * Открыть туннель до базы `db1` в кластере `mdb8fb15nf1vr2qlu1in` в **тестинге**:

    `h2p pg-mdb8fb15nf1vr2qlu1in@db1 -t`

  * Сделать SQL запрос к базе `db1` в кластере `mdba7mivql6v0aee7uev` **в режиме только чтение**:

    `h2p pg-mdba7mivql6v0aee7uev@db1 'SELECT 1;'`

  * Сделать SQL запрос к базе `db1` в кластере `mdba7mivql6v0aee7uev` **с возможностью записи**:

    `h2p pg-mdba7mivql6v0aee7uev@db1 'UPDATE users SET column1 = 1 WHERE column2 = 2;'`

{% endlist %}


## Changelog

{% cut "1.13" %}

* Добавили поддержку баз `PostgreSQL` в MDB

{% endcut %}

{% cut "1.12" %}

* Добавили возможность ходить в тестинг по ключику `-t`
* Убрали поддержку MySQL на железе - все кластера переехали в MDB

{% endcut %}

{% cut "1.11" %}

* Починили переопределение имени пользователя через `H2P_USER`
* Починили баг, при котором запрашивалась всегда `rw` роль в базу данных в первый раз

{% endcut %}

{% cut "1.10" %}

* Если у вас старая версия `cli` - выведется предупреждение. Сам клиент продолжит работу в обычном режиме
* После заказа и подтверждения роли ждем пока IDM добавит ее в свою базу (несколько секунд) перед тем, как пускать туда трафик
* Если у вас есть активный `rw` доступ в базу данных, то теперь вы можете подключиться и в `ro` режиме (без флага `-w`)
* Больше отладочной информации о SSH ключах в агенте (при запуске с опцией `-v`)

{% endcut %}

{% cut "1.9" %}

* Теперь выводим версию по флагу `--version`
* Перебираем все датацентры в Консуле, чтобы найти сервис. Отпала необходимость явно указывать дц при хождении в конкретный аллокейшн
* Исправили работу с SSH соединениями. Раньше, если сделать много запросов подряд, вылезала ошибка `Too many open files`
* Стали вести этот changelog :)

{% endcut %}

