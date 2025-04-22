# Быстрый старт в Go


## Аркадия {#arc_mount}
Аркадия — общий репозиторий Яндекса. Код Морды живёт в директории [portal](https://a.yandex-team.ru/arc/trunk/arcadia/portal).

1. Для работы с Аркадией установите систему контроля вресий **Arc** и утилиту **ya** [по инструкции](https://docs.yandex-team.ru/devtools/intro/quick-start-guide).

2. Смонтируйте репозиторий Аркадии:
    ```
    mkdir -p ~/arcadia ~/store
    arc mount -m ~/arcadia -S ~/store
    ```
{% note info %}

В дальнейших примерах предполагается, что репозиторий был установлен в домашнюю директорию пользователя ``~/arcadia``

{% endnote %}

*Еще по теме: [Правила разработки в Аркадии на Go](https://wiki.yandex-team.ru/devrules/Go)*

## GoLand

Goland — популярная IDE для разработки на Go. Дальнейшая инструкция будет приведена для этой среды разработки.
1. [Скачайте](https://www.jetbrains.com/go) и [активируйте](https://wiki.yandex-team.ru/jetbrains/licenseservers) GoLand
1. Создайте проект из пресета с помощью утилиты **ya**:
    ```
    cd ~/arcadia
    ya ide goland portal
    ```
   Для ускорения работы IDE, мы явно указали путь, который нужно индексировать (папка проекта Морды в Аркадии - portal).

1. Теперь можно запустить GoLand и открыть созданный проект, который находится в директории ``arcadia``

1. Рекомендуется установить [плагин для работы с Аркадией](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#jb-plugin-setup)

1. Можно настроить автоматическое подключение репозитория при каждом старте GoLand, чтобы не подключать его вручную после каждого рестарта системы.
   В разделе **File — Settings (Ctrl + Alt + S) — Tools — Startup Tasks**
   добавьте задачу типа **Shell Script**:
    * **Execute:** Script text
    * **Script text:** ``arc status | grep 'Not an arc repository' && arc mount -m . -S ../store``
    * **Working dirctory:** ``~/arcadia``

## Тулинг

Добавим в PATH путь к Аркадийному тулингу:
```
export GOROOT=$(ya tool go --print-toolchain-path)
export PATH=$GOROOT/bin:$PATH
```
В Go существуют общепринятые инструменты для автоматического форматирования кода **gofmt** и **goimports**. Для нас они доступны через утлиту **ya tool**.
Рекомендуется использовать утилиту yoimports, которая обхединяет их обе и еще некоторые специфические вещи.

Можно настроить автоматический запуск этих инструментов при каждом сохранении файла:

{% list tabs %}

- gofmt
    1. **File — Settings (Ctrl + Alt + S) — Tools — File Watchers**
    1. Создать новое правило нажав на + и выбрать ``go fmt``
    1. В октрывшемся окне изменить поля:
        * **Scope:** Current File
        * **Program:** ``~/arcadia/ya``
        * **Arguments:** ``tool gofmt -w \$FilePath\$``


- yoimports (goimports)
    1. Settings (Ctrl + Alt + S) — Tools — File Watchers
    2. Создать новое правило нажав на + и выбрать ``yoimports``
    3. В октрывшемся окне изменить поля:
        * **Scope:** Current File
        * **Program:** ``~/arcadia/ya``
        * **Arguments:** ``tool yoimports -w \$FilePath\$``


{% endlist %}


Утилиты будут запускатья при сохранениия файла по Ctrl&nbsp;+&nbsp;S. Чтобы они запускались автоматически при каждом изменении файла, на последнем шаге можно отметить чекбокс **"Auto-save edited files to trigger the watcher"**.

*Еще по настройке IDE: [Goland](https://wiki.yandex-team.ru/mdb/internal/teams/core/development/goland)*

*Еще по теме: [Список инструментов ya](https://docs.yandex-team.ru/yatool/tools/list)*

## Компиляция

Для сборки проекта используется утилита ya make. Утилита работает рекурсивно, поэтому рекомендуется запускать ее только из директории проекта, который нужно скомпилировать. Пример для сборки исполняемого файла **morda-go**:

```
cd portal/morda-go/cmd/morda-go
ya make
```
Исполняемый файл **morda-go** будет доступен по пути ``portal/morda-go/cmd/morda-go/morda-go``

Перед началом работы рекомендуется сгенерировать необходимые .go файлы из протобафа. Если этого не сделать, IDE будет ругаться на импорты:
```
ya make -k -j 4 --add-result go
```
Команду нужно запускать из корневой директории проекта **portal** либо, для ускорения, только в директориях, которые содержат protobuf-файлы.

*Еще по теме: [Руководство по сборке кода на Go](https://docs.yandex-team.ru/ya-make/tutorials/go)*

## Запуск

{% note info %}

Поднимать инстансы для отладки лучше на дев-хостах, так как там уже есть необходимые доступы.

{% endnote %}

{% note warning %}

Для запуска нужна геобаза. Она уже есть на дев-хосте, нужно только скопировать:
```
cp /opt/www/bases/geodata50.bin /var/cache/geobase/geodata5.bin
```
{% endnote %}

**morda-go:**
```./morda-go -apphost=20223```


## Настройка SSH {#ssh}
Так как запуск и отладка будет проводиться на удаленном сервере, в GoLand нужно добавить SSH-конфигурацию и использовать ее при деплое:

**File — Settings (Ctrl + Alt + S) — Tools — SSH Configuration**

![SSH Configuration](https://jing.yandex-team.ru/files/slindgre/Settings_002.png)


## Дебаг

Дебажить в Go можно с помощию утилиты **ya tool dlv**.


### Сборка
Рассмотрим два подхода на примере **morda-go**:

{% list tabs %}
- Удаленная сборка

  **Плюсы:** скорость

  **Минусы:** нужна синхронизация репозитория с удаленным сервером. Это не очень надежно: у синхронизации есть задержки, она иногда рвется и приходится настраивать заново.

    1. На удаленном сервере выполните
        ```
        sudo modprobe fuse
        ```
    1. [Смонтируйте репозиторий](#arc_mount) Аркадии например в ``/opt/www/arcadia/src/a.yandex-team.ru``. Для создания новых объектов в ``/opt/www`` нужно выполнить следующую команду: ``sudo chown -R <user_name> /opt/www``.
    1. Настройте синхронизацию локального репозитория с репозиторием на удаленном сервере. Выполните из корня репозитория ``~/arcadia``:
        ```
        arc sync --remote-follow morda-dev-v999.sas.yp-c.yandex.net:/opt/www/arcadia/src/a.yandex-team.ru
        ```
    1. Создайте экшн **"morda-go build remote"** на удаленую сборку проекта

       **File — Settings (Ctrl + Alt + S) — Tools — Remote SSH External Tools**

        * **Program:** ``ya``
        * **Arguments:** ``make portal/morda-go/cmd/morda-go -DGO_COMPILE_FLAGS_VALUE="-N -l"``
        * **Working directory:** ``/opt/www/arcadia/src/a.yandex-team.ru``
        * **SSH configuration:** выбрать конфигурацию, которую [настроили ранее](#ssh)

       {% cut "Пример" %}

       ![morda-go build remote](https://jing.yandex-team.ru/files/slindgre/Edit%20Tool_006.png)

       {% endcut %}
- Локальная сборка

  **Плюсы:** надежность, так как локально всегда актуальный код.

  **Минусы:** медленнее, так как исполняемый файл копируется на удленный сервер.

    1. Создайте экшн **"morda-go build local"** на локальную сборку проекта

       **File — Settings (Ctrl + Alt + S) — Tools — External Tools**

        * **Program:** ``~/arcadia/ya``
        * **Arguments:** ``make portal/morda-go/cmd/morda-go -DGO_COMPILE_FLAGS_VALUE="-N -l" --add-result go``
        * **Working directory:** ``~/arcadia``

       {% cut "Пример" %}

       ![morda-go build local](https://jing.yandex-team.ru/files/slindgre/Edit%20Tool_007.png)

       {% endcut %}

    1. Создайте экшн **"morda-go copy remote"** для копирования бинарного файла на удаленный сервер

       **File — Settings (Ctrl + Alt + S) — Tools — External Tools**

        * **Program:** ``scp``
        * **Arguments:** ``portal/morda-go/cmd/morda-go/morda-go user_name@morda-dev-v999.sas.yp-c.yandex.net:/opt/www/arcadia/src/a.yandex-team.ru/portal/morda-go/cmd/morda-go``
        * **Working directory:** ``~/arcadia``

       {% cut "Пример" %}

       ![morda-go copy remote](https://jing.yandex-team.ru/files/slindgre/Edit%20Tool_003.png)

       {% endcut %}

{% endlist %}

### Настройка dlv
Создайте экшн **"morda-go dlv remote"** на запуск **dlv** на удаленном сервере.

**File — Settings (Ctrl + Alt + S) — Tools — Remote SSH External Tools**
* **Program:** ``/bin/bash``
* **Arguments:** ``-c
  "nohup `ya tool dlv --print-path` --headless=true --listen=:27000 --api-version=2 exec portal/morda-go/cmd/morda-go/morda-go -- -apphost=20223 & sleep 1s"``
* **Working directory:** ``/opt/www/arcadia/src/a.yandex-team.ru``
* **SSH configuration:** выбрать конфигурацию, которую [настроили ранее](#ssh)

{% cut "Пример" %}

![morda-go dlv remote](https://jing.yandex-team.ru/files/slindgre/Edit%20Tool_008.png)

{% endcut %}

{% cut "Пока не работает удаленный запуск dlv" %}

- Отключаем экшн **"morda-go dlv remote"**
- На сервере из корневой папки аркадии запускаем `` `ya tool dlv --print-path` --headless=true --listen=:27000 --api-version=2 exec portal/morda-go/cmd/morda-go/morda-go -- -apphost=20223``
- Следуем инструкции дальше

Перед каждым запуском нужно сперва запустить dlv руками.

{% endcut %}

### Пайплан

GoLand позволяет создавать пайплайны из экшенов, чтобы запускать процесс деплоя одним кликом.

**Run — Edit Configurations**
- **Name:** morda-go debug
- **Host:** morda-dev-v999.sas.yp-c.yandex.net
- **Port:** 27000
- **Before launch**: добавьте экшены в заданном порядке

  {% list tabs %}

    - Удаленная сборка

        1. morda-go build remote
        1. morda-go dlv remote

      ![morda-go debug](https://jing.yandex-team.ru/files/slindgre/Run-Debug%20Configurations_003.png)

    - Локальная сборка

        1. morda-go build local
        1. morda-go copy remote
        1. morda-go dlv remote

      ![morda-go debug](https://jing.yandex-team.ru/files/slindgre/Run-Debug%20Configurations_001.png)

  {% endlist %}

### Запуск
Теперь можно расставить в коде точки останова, выбрать пайплайн **"morda-go debug"** из дебаг-панели в правом верхнем углу и запустить его (Shift + F9).

![debug panel](https://jing.yandex-team.ru/files/slindgre/Selection_008-1.png)

После остановки дебага (Ctrl + F2) процессы **dlv** и **morda-go** на удаленном сервере будут завершены автоматически.

*Еще по теме: [Удаленная отладка Go в GoLand](https://wiki.yandex-team.ru/mds/dev/goland-remote-debug-setup/)*

## Тесты

Тесты запускаются **из директории проекта** и проходят рекурсиво по вложенным папкам. 
Для запуска тестов надо выполнить команду: 

`ya make -t` для маленьких (small) тестов 

`ya make -tt` для средних, 

`ya make -ttt` или `ya make -A` для всех тестов.




