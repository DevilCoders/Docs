# Разработка в песочницах

Для отладки и тестирования изменений в сервере и шедьюлере Огорода можно использовать песочницы.

## Где проводить

Песочницы могут работать только на специально подготовленных дев-машинах. В данный момент доступны следующие:

hostname | UI
--- | ---
wicket.sas.yp-c.yandex.net | [https://wicket.dev.maps.yandex-team.ru/](https://wicket.dev.maps.yandex-team.ru/)

## Доступы

### SSH

К дев-машинам ssh-доступ технически ограничен только для разработчиков, зарегистрированных в abc-сервисе
[maps-qyp-garden](https://abc.yandex-team.ru/services/maps-qyp-garden).
Расширение списка делается без ограничений по запросу из ABC UI или в телеграм чате "Garden Helpdesk".

Для запуска песочниц потребуется правильная настройка `ssh-agent` (ssh-подпись будет использоваться для получения секретов из Секретницы
и для получение OAuth-токена для доступа к Огороду).

### Docker

docker нужен для запуска образа Огорода.

#### Настройка аккаунта на машине плейгранда

Для работы с docker пользовательский логин должен быть в группе `docker`.
```bash
# add yourself to the docker group
$ sudo adduser $USER docker
```
После добавления аккаунта в группу необходимо перелогиниться.

#### Настройка доступа к [Docker Registry](https://wiki.yandex-team.ru/qloud/docker-registry)

```bash
$ docker login registry.yandex.net -u $USER -p <your_token>
```
`<your_token>` можно получить по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1).

#### Проверка работы с docker

После успешной регистрации аккаунта, следущая команда должна выполниться успешно:
```bash
$ docker pull registry.yandex.net/ubuntu:bionic
```

## Работа с песочницей

### Первоначальные настройки

Все песочницы должны создаваться строго в директории `~/play`.
```bash
$ mkdir ~/play && cd ~/play
```

### Создание конфигурации

```bash
$ cd ~/play
$ garden-playground setup <playground_name_suffix>
```

Полное имя песочницы будет: `<login>_<playground_name_suffix>`.

Данная команда создаст директорию `~/play/<playground_name>`, заполнив ее файлами с первоначальной конфигурацией.

TODO: описать работу с конфигами и секретами в песочницах.

### Запуск песочницы

Песочница включает 2 докер-контейнера: с сервером и шедьюлером. Их нужно запускать одновременно в разных терминалах.

Перейти в директорию песочницы и выполнить команду:
```bash
$ cd ~/play/<playground_name>
$ garden-playground run
```

Будет предложено выбрать, запускать сервер или шедьюлер. Далее команда запустит shell внутри докер-контейнера.

Из командной строки можно обновить версии модулей или изменить конфигурацию (подробнее ниже), после чего нужно запустить сервер или шедьюлер.

Сервер:
```bash
container# /scripts/run_garden_server.sh
```

Шедьюлер:
```bash
container# /scripts/run_garden_scheduler.sh
```

После старта сервера ссылка на UI песочницы доступна в списке "Active playgrounds" в UI дев-машины.
Пример:
* [https://wicket.dev.maps.yandex-team.ru/](https://wicket.dev.maps.yandex-team.ru/) - страница со списком "Active playgrounds"
* https://<playground_name>.wicket.dev.maps.yandex-team.ru:8443/ - URL для UI песочницы.
* https://<playground_name>.wicket.dev.maps.yandex-team.ru/ - URL для API сервера.

Логи запущенного сервера доступны в директории `~/play/<playground_name>/work/log`.

### Запуск песочницы в фоне

Обычно требуется, чтобы песочница работала длительное время (часы или дни), чтобы разработчик мог запустить какие-то длительные процессы в фоне и уйти домой.

Для этого можно использовать утилиты `screen` или `tmux`. Ниже приведён пример запуска через `tmux`:

```bash
# Создать новую сессию. Имя сессии можно сделать таким же, как имя песочницы
tmux new-session -s <playground_name> -c ~/play/<playground_name>/
# Запустить сервер
garden-playground run
/scripts/run_garden_server.sh
# Разделить экран на 2 части
Ctrl+b %
# Запустить шедьюлер
garden-playground run
/scripts/run_garden_scheduler.sh
# Отключиться от tmux - он останется работать в фоне
Ctrl+b d

# При необходимости подключиться к запущенной сессии tmux
tmux attach-session -t <playground_name>
```

### Альтернативный вариант запуска песочницы в фоне
1. Запускаем плейгранд командой garden-playground run дважды - первый раз запускаем сервер, второй раз запускаем скедулер
и тут же выходим. После запуска в списке контейнеров докера появятся два контейнера <playground_name>_server и
<playground_name>_scheduler
2. Запускаем оба контейнера, чтоб работали постоянно командой:
```bash
docker start <playground_name>_server <playground_name>_scheduler
```
3. Подключаемся к каждому контейнеру командой:
```bash
docker exec -it <playground_name>_scheduler "bash"
# или:
docker exec -it <playground_name>_server "bash"
```
4. Для сервера исправляем скрипт `/scripts/run_garden_server.sh`.
Комментируем строчку с запуском сервера и вместо неё добавляем строки:
```bash
export Y_PYTHON_SOURCE_ROOT=/home/<login>/<arcadia_path>
sudo --user www-data --preserve-env /home/<login>/<arcadia_path>/maps/garden/server/bin/garden-server 2>&1 | tee /var/log/garden.log
```
Если хотим, чтоб сервер работал в фоне, запускаем весь скрипт в фоне:
```bash
/scripts/run_garden_server.sh &
```
И отключаемся от контейнера с помощью `Ctrl+d`.

5. Для скедулера проделываем аналогичную операцию. Правим скрипт `/scripts/run_garden_scheduler.sh`.
Комментируем строчку с запуском скедулера и вместо неё добавляем строки:
```bash
export Y_PYTHON_SOURCE_ROOT=/home/<login>/<arcadia_path>
sudo --user www-data --preserve-env /home/<login>/<arcadia_path>/maps/garden/heduler/bin/garden-scheduler 2>&1 | tee /var/log/garden.log
```
Если хотим, чтоб сервер работал в фоне, запускаем весь скрипт в фоне:
```bash
/scripts/run_garden_scheduler.sh &
```
И отключаемся от контейнера с помощью `Ctrl+d`.

6. Для перезапуска сервера или скедулера, если они запущены в фоне, надо перезапустить контейнер командой `docker restart <playground_name>_<server|scheduler>`,
Зайти обратно в контейнер и опять запустить скрипт. Альтернативный вариант - запускать скрипт без `&` в скрине, например.

Этот способ избавляет от необходимости собирать бинарник - питоновские исходники подхватываются с файловой системы, а так
же от необходимости копировать бинарник в докер.


### Добавление исходных данных

Чтобы добавить исходные данные в песочницу, можно использовать механизм [сканирования ресурсов](scan_resources.md),
либо добавить данные вручную по инструкции:

1. Данные загружаются в любое хранилище, откуда они могут быть загружены по http (например, в Sandbox или MDS).

2. Подготавливаются данные для http запроса для создания билда с указанием:

    * имени контура в поле `contour_name`
    * внешнего ключа в поле `foreign_key`: это поле позволит Огороду проверить,
    не был ли билд с такими же ресурсами добавлен ранее. К ключу предъявляются
    следующие требования:
        * он должен выбираться таким, чтобы по нему можно было однозначно
        идентифицировать билд во внешней системе (например, для `ymapsdf_src`
        это номер таски экспорта и название региона)
        * он должен представлять собой набор ключей со строковыми
        значениями (то есть, не иметь вложенных структур)
    * списка ресурсов в поле `resources`. Для каждого ресурса
    необходимо указать:
        * имя ресурса в поле `name`: по нему Огород найдёт необходимый прообраз
        ресурса в графе
        * свойства ресурса в поле `version.properties`
        (например, `shipping_date`, список файлов, регион): эти свойства Огород
        сделает частью создаваемого ресурса

    Пример:

    ```json
    {
        "contour": "user_test_new_feature",
        "foreign_key": {
            "nmaps_export_task_id": "272482",
            "region": "cis1"
        },
        "resources": [
            {
                "name": "src_url_cis1_yandex",
                "version": {
                    "properties": {
                        "file_list": [
                            {
                              "url": "http://storage-int.mds.yandex.net:80/get-mpro-dataset/50206/export_cis1/20190801_365638_1192_145654057/cis1/ymapsdf2.dump.gz.tar",
                              "name": "ymapsdf2.dump.gz.tar"
                            },
                            {
                              "url": "http://storage-int.mds.yandex.net:80/get-mpro-dataset/1658545/export_aao/20190801_365638_1192_145654057/aao/ymapsdf2.schema.tar",
                              "name": "ymapsdf2.schema.tar"
                            }
                        ],
                        "shipping_date": "20181204_272482_943_112382961",
                        "region": "cis1",
                        "vendor": "yandex",
                        "nmaps_branch_id": "943"
                    }
                }
            }
        ]
    }
    ```

3. Посылается http post запрос в Огородный сервер песочницы, передав в него подготовленный на шаге 2 json-файл.

    ```bash
    $ curl -X POST -H "Authorization: OAuth <OAuth-токен>" -H "Content-Type: application/json" https://<playground_name>.wicket.dev.maps.yandex-team.ru/modules/<module_name>/builds/ --data @data.json
    ```

## Обновление бинарников сервера или шедьюлера

Вариант 1: с хост-системы скопировать ссылку на бинарник сервера или шедьюлера в докер-контейнер.

Сервер:
```bash
cd maps/garden/server/bin
ya make -r
docker cp garden-server <playground_name>_server:/usr/bin/garden-server
```

Шедьюлер:
```bash
cd maps/garden/scheduler/bin
ya make -r
docker cp garden-scheduler <playground_name>_scheduler:/usr/bin/garden-scheduler
```

Вариант 2: внутри докер-конейтера поправить скрипты `/scripts/run_garden_server.sh` и `/scripts/run_garden_scheduler.sh`, где указать путь к нужным бинарникам в Аркадии. При этом репозиторий `arc` должен быть смонтирован с опцией `--allow-other` ([подробнее](https://doc.yandex-team.ru/arc/manual/arc/commands.html#arc-mount)).

### Ускорение запуска

Чтобы не тратить время на пересборку бинарников каждый раз командой `ya make -r`, можно настроить запуск так, чтобы единожды собранные бинарники подхватывали все изменения py-файлов прямо из репозитория.

Для этого в скриптах `/scripts/run_garden_server.sh` и `/scripts/run_garden_scheduler.sh` нужно вписать строчку:
```bash
export Y_PYTHON_SOURCE_ROOT=/home/<login>/arc/arcadia
```

[Подробнее](https://docs.yandex-team.ru/ya-make/manual/python/vars#y_python_source_root)

## Обновление версии модуля

1. Соберите бинарный модуль.

2. Зарегистрируйте и активизируйте модуль.

    С хоста песочницы:
    ```bash
    $ garden-playground upload ~/play/<playground_name> -p <path_to_module_binary>
    ```

Команда `garden-playground upload` автоматически создаёт новый дев-контур `<login>_test` и заливает в него модуль.

Если нужно залить модуль в любой другой дев-контур, то можно воспользоваться общим тулом `garden`:
```bash
garden module -e development -s <playgroun_name>.wicket.dev.maps.yandex-team.ru upload -p <path_to_module_binary> -c <contour_name> -m "<Message>"
```

## Обновление докер образов

Обновление докер-образов Огорода на последние версии делается командой:
```bash
$ garden-playground update ~/play/<playground_name>
```

{% note warning "Attention" %}

При обновлении образа все изменения, которые были сделаны в файловой системе контейнера, потеряются, их нужно будет заново применять. Изменения в Монге и других внешних системах (S3, YT) сохранятся.

{% endnote %}


## Удаление песочницы

```bash
$ garden-playground remove ~/play/<playground_name>
```
Данный скрипт удалит данные из некоторых внешних систем (YT и S3) и директорию песочницы в `~/play`.

{% note warning "Attention" %}

При удалении не удаляются ресурсы из других внешних систем (Sandbox, ecstatic).

{% endnote %}

## Ссылки

### Ресурсы

* YT: поддиректория ```<playground_name>``` в директории [//home/maps/core/garden-exp](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden-exp)
* Ecstatic: [http://core-ecstatic-coordinator.common.unstable.maps.yandex.net/pkg/list](http://core-ecstatic-coordinator.common.unstable.maps.yandex.net/pkg/list)
