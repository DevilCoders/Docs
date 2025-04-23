# Собственная инсталляции Sandbox

{% note alert %}

Использование собственной инсталляции Sandbox не рекомендуется в силу сложности настройки и поддержания работоспособности всех службы Sandbox.
Оптимальным вариантом является разработка бинарной задачи и отладка её на общем Sandbox, как описано в [разделе про бинарные задачи](binary-task.md).

{% endnote %}

Установить Sandbox на ноутбук нельзя, поскольку он требует наличия сервисов Skynet,
которые нельзя запустить без наличия DNS-записи и дырок до Skynet-трекеров.



## Запуск виртуальной машины из образа в QYP { #vm-launch }

Для локальной отладки нам потребуется запустить собственный Sandbox.
Sandbox - сервис с множеством зависимостей (в том числе от сервисов Skynet), поэтому развертывание на ноутбуке невозможно.
Для запуска лучше всего использовать виртуальную машину, образ которой был подготовлен командой Sandbox.
Покажем, как это сделать:

1. Открываем облако [QYP](https://qyp.yandex-team.ru/) и нажимаем [Launch new VM](https://qyp.yandex-team.ru/create-vm).

2. Вводим имя виртуальной машины и выбираем сеть `_SEARCHSAND_`

    {% cut "Скриншот" %}

    ![Имя и сеть виртуальной машины](img/debug-local-name.png "Имя и сеть виртуальной машины")

    {% endcut %}

3. Указываем свой проект в [ABC](https://abc.yandex-team.ru/) и датацентр, где будет запущена виртуальная машина:

    {% cut "Скриншот" %}

    ![Квота и датацентр](img/debug-local-quota.png "Квота и датацентр")

    {% endcut %}

4. Выбираем доступные вычислительные ресурсы (количество процессорных ядер, оперативной памяти, тип и размер жесткого диска).
    Рекомендуется иметь не менее 4 ядер, 16 Гб памяти и 200 Гб SSD диска.

    {% cut "Скриншот" %}

    ![Вычислительные ресурсы](img/debug-local-resources.png "Вычислительные ресурсы")

    {% endcut %}

5. В том же разделе указываем ресурс, содержащий образ виртуальной машины с Sandbox.
    Нужно брать последнюю стабильную версию ресурса
    [QEMU_IMAGE_SANDBOX](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=QEMU_IMAGE_SANDBOX&state=READY&attrs=%7B%22released%22%3A%22stable%22%7D&limit=1)
    и копировать значение из поля **Skynet ID** (rbtorrent). Тип образа должен быть **QCOW2**.

6. Включаем доступ в Интернет через NAT64. Указываем пользователей, которые имеют доступ к виртуальной машине.
    Нажимаем **Create** и дожидаемся пока машина запустится.

    {% cut "Скриншот" %}

    ![Пользователи](img/debug-local-users.png "Пользователи")

    {% endcut %}

7. Заходим на виртуальную машину по SSH. Следует скопировать FQDN со страницы вашей виртуалки.

    ```bash
    $ ssh sandbox-test-vm.sas.yp-c.yandex.net
    ```

8. Устанавливаем Arc как описано в разделе [Быстрый старт](/devtools/intro/quick-start-guide):

    ```bash
    $ echo 'alias python=/usr/bin/python3' >> ~/.bashrc && source ~/.bashrc
    $ export ARC_TOKEN='AQAD-...'
    $ mkdir -p ~/.arc
    $ chmod 700 ~/.arc
    $ echo -n $ARC_TOKEN > ~/.arc/token
    $ chmod 400 ~/.arc/token
    $ sudo apt update
    $ sudo apt -y install yandex-arc-launcher
    ```

9. Убеждаемся, что в файле `/etc/fuse.conf` есть строчка `user_allow_other` и монтируем единый репозиторий:

    ```bash
    $ mkdir -p arcadia store
    $ arc mount -m arcadia/ -S store/ --allow-root
    ```

    {% note warning %}

    Флаг `--allow-root` важен! Без него Sandbox запустится не полностью и клиенты будут недоступны.

    {% endnote %}

10. Чтобы `arc` работал быстрее, отключаем создание файлов Python файлов `.pyc` и `.pyo`:

    ```bash
    $ echo 'export PYTHONDONTWRITEBYTECODE=1' >> ~/.bashrc && source ~/.bashrc
    ```


11. Добавляем команду `sandbox` в PATH:

    ```bash
    $ echo 'alias sandbox="$HOME/arcadia/sandbox/sandbox"' >> ~/.bashrc && source ~/.bashrc
    ```

12. Запускаем Sandbox на порту 8000:

    ```bash
    $ sandbox setup -p 8000
    $ sandbox start
    ```

    Чтобы использовать нестандартный порт MongoDB, можно воспользоваться аргументом запуска `--mongo-uri`.

    ```bash
    $ sandbox setup -p 8000 --mongo-uri "mongodb://localhost:12345/sandbox"
    ```
    При выборе порта Sandbox нужно учитывать, что для работы локальных сервисов необходимы порты в диапазоне `[port, port+10]`.

    Другие аргументы запуска можно посмортеть в помощи `sandbox setup -h`

    Теперь можно открыть веб-интерфейс Sandbox на порту 8000, например, `http://sandbox-test-vm.sas.yp-c.yandex.net:8000`.

## Самостоятельная настройка окружения { #setup-environment }

{% note alert %}

Мы не рекомендуем настраивать окружение самостоятельно, так как расследование проблем в случае ошибки требует значительных усилий
со стороны разработчика и зачастую невозможно без привлечения команды Sandbox.

{% endnote %}

Для создания окружения, в котором сможет работать локальный Sandbox, надо повторить те же шаги, что и при создании
[текущего образа](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=QEMU_IMAGE_SANDBOX&state=READY&attrs=%7B%22released%22%3A%22stable%22%7D&limit=1).
Сами шаги заданы в параметрах задачи, создавшей образ. Если вкратце, то надо повторить операции
[из скрипта sandbox/scripts/dev/qemu-sandbox-step.sh](https://a.yandex-team.ru/arc_vcs/sandbox/scripts/dev/qemu-sandbox-step.sh)
на хосте с Ubuntu Xenial.


{% cut "Подробнее" %}

#### OS

Рекомендуется использовать Linux Ubuntu 16.04 Xenial. С версией ядра старше 3.
Работоспособность Sandbox в других версиях Linux не проверялась.

#### Skynet
Наличие сервисов Skynet обязательно. Проверить версию скайнета можно следующим образом:
```bash
$ sky --version
Version: 17.2.15
```
Если команда не отрабатывает, обратитесь к администратору сервера — скорее всего, на машине Skynet сломан или отсутствует.
Кроме этого, директория, куда вы устанавливаете Sandbox, должна быть открыта для чтения пользователю skynet.

Sandbox ожидает наличия директорий:
```bash
$ ls -la /Berkanavt /skynet
lrwxrwxrwx 1 root root 16 Jan 24 16:50 /Berkanavt -> /place/berkanavt
lrwxrwxrwx 1 root root 33 Oct 23  2018 /skynet -> /Berkanavt/supervisor/base/active
```
Если они представлены символическими ссылками, убедитесь что они указывают на абсолютные, а не относительные пути.

#### cgroup

Наличие си-групп обязательно. Установить их можно при помощи пакета `cgroup-lite`.

#### MongoDB

Рекомендуется версия 3.6.4 или более новая.

#### resolv.conf { #dns }

[Основная статья](cookbook.md#dns)

Чтобы тестировать задачи с параметром `dns=DNS64`, необходим файл `/etc/resolv.conf.dns64` с содержимым:
```
search search.yandex.net yandex.ru
nameserver 2a02:6b8:0:3400::5005
nameserver 2a02:6b8:0:3400::5005
```
(дублирование адресов здесь [не просто так](https://st.yandex-team.ru/SANDBOX-3815#1487699348000))

Можно создать с этими же строками файл `/etc/resolv.conf.dns64`, тогда локальный сэндбокс будет переключать конфиги в зависимости от значения поля `dns` в задаче.

#### locale

Убедитесь, что команда `locale` не выводит ошибки вида `No such file or directory`: все выставленные локали должны быть сгенерированы.


#### LXC

{% note warning %}

[LXC](https://ru.wikipedia.org/wiki/LXC) и [Porto](https://wiki.yandex-team.ru/porto/) не уживаются на одном хосте.
Поэтому, если вы пользуетесь Porto, про LXC придётся забыть, и наоборот.

{% endnote %}

LXC установливается пакетом `lxc`. Также для его работы необходим **беспарольный sudo**.


#### Доступы
Заказываются через [Puncher](https://puncher.yandex-team.ru).

С разработческого сервера должен быть доступ до **sandbox-ui.s3.mds.yandex.net** (TCP 80, 443).

{% endcut %}

## Управление локальным Sandbox { #manage }

* Sandbox перезапускается автоматически при любых изменениях кода (в том числе кода задач).
  Чтобы отключить это поведение, нужно отредактировать файл `arcadia/../runtime_data/configs/settings.yaml`
  (создается при выполнении `sandbox setup`):

    ```yaml
    server:
      autoreload: false
    ```
    Полный набор поддерживаемых параметров можно посмотреть [в дефолтном конфиге](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/etc/.settings.yaml).

* Если автоматический перезапуск отключен, перечитать изменения можно, перезапустив сервер Sandbox и агента:

    ```bash
    $ sandbox restart
    ```

* По умолчанию Sandbox на виртуальной машине может запускать **только 1 задачу одновременно**.
    Чтобы запускать несколько задач параллельно, нужно добавить ещё одну настройку в `~/runtime_data/configs/settings.yaml`:

    ```yaml
    client:
      max_job_slots: 7
    ```

* По умолчанию, по завершении задачи, все файлы в рабочей директории задачи, не являющиеся ресурсами, удаляются.
    Чтобы отключить это поведение, добавьте ещё один параметр в тот же файл:

    ```yaml
    client:
      auto_cleanup:
        on_task_finish: false
    ```

* Если вам требуется отлаживать задачи, требующие прав root (`privileged = True`), то по умолчанию для таких задач,
    LXC-контейнер каждый раз собирается заново. Чтобы ускорить отладку, можно выставить параметр:

    ```yaml
    client:
      lxc:
        keep_privileged: true
    ```

    В этом случае все задачи будут использовать один и тот же контейнер, собранный при запуске первой задачи.
    Чтобы уничтожить контейнер, используйте команду:

    ```bash
    $ sandbox destroy_container
    ```

* Чтобы остановить все компоненты Sandbox:

    ```bash
    $ sandbox kill
    ```

    Например, чтобы обновить код самого Sandbox до последнего коммита в репозитории:

    ```bash
    $ sandbox kill
    $ cd ~/arcadia
    $ arc pull
    $ sandbox start
    ```

* Чтобы полностью удалить Sandbox (остановить Sandbox, очистить базу данных и удалить конфигурационные файлы):

    ```bash
    $ sandbox clean_all
    ```

## Отладка задач в локальном Sandbox { #debug-task }

Для отладки кода задачи:

1. Внесите изменения в код задач прямо на виртуальной машине (в `~/arcadia/sandbox/projects`) или используйте [arc-sync](https://docs.yandex-team.ru/arc/ref/commands#sync).
2. Sandbox автоматически перезагрузится. Если в коде задач есть критическая ошибка, то сервер может упасть. В этом случае нужно внести исправления и запустить сервер заново.
3. Запустите задачу и убедитесь, что она работает так, как предполагалось.
4. Чтобы выполнить тесты кода всех задач на виртуальной машине, используйте команду:

    ```bash
    $ sandbox test_tasks
    ```

Существует возможность создать задачу в состоянии **DRAFT**, скопировав её и все необходимые ресурсы из основного кластера Sandbox:

```bash
$ sandbox clone_task --id 48348515
...
2016-01-29 19:38:34,170 INFO (sandbox_ctl) Task #48348515 with 5 dependencies was successfully cloned from production Sandbox and saved as DRAFT with id #5.
```

Можно просто импортировать описание задачи и её ресурсы из основного кластера Sandbox:

```bash
$ sandbox add_task --id 20520995  # Добавит задачу 20520995 и все её ресурсы
$ sandbox add_resource --id 39045097  # Добавит задачу, создавшую ресурс 39045097, и все остальные её ресурсы
```

## Отладка бинарных задач в локальной инсталляции { #binary-tasks }

В локальном Sandbox можно отлаживать бинарные задачи:

```bash
$ sandbox upload_binary projects/my-team/my-task --enable-taskbox --attr released=stable --url http://sandbox-test-vm.sas.yp-c.yandex.net:8000
Check input file ... Done. [00s]
Prepare resource attributes ... Done. [00s]
Create parent task ... Done. [00s]
Create resource ... Done. [00s]
Copy file content ... Done. [00s]
Binary tasks resource: http://sandbox-test-vm.sas.yp-c.yandex.net:8000/resource/310
```

То же самое можно сделать запуская исполняемый файл, добавив `--skynet` и `--no-auth` к аргументам запуска. Файл будет сначала загружен в Skynet, а потом импортирован в локальный Sandbox с помощью задачи `REMOTE_COPY_RESOURCE`. Этот способ более медленный.

```bash
~/arcadia/sandbox/projects/my-team/my-task$ ./my-task run --no-auth --skynet --url "http://sandbox-test-vm.sas.yp-c.yandex.net:8000" --create-only --type MY_TEST_TASK
2018-11-22 17:03:37	INFO	1 file (58.31MiB) to upload
2018-11-22 17:03:37	INFO	Uploading task #53 created: http://sandbox-test-vm.sas.yp-c.yandex.net:8000/task/53
2018-11-22 17:03:58	INFO	Task is in EXECUTING state
2018-11-22 17:04:07	INFO	Task is in FINISHING state
2018-11-22 17:04:10	INFO	Task is in SUCCESS state
2018-11-22 17:04:11	INFO	Task of type MY_TEST_TASK created: http://http://sandbox-test-vm.sas.yp-c.yandex.net:8000/task/54
```

Больше про интерфейс командной строки бинарных задач можно посмотреть [тут](binary-task.md#cli-mode)

## Отладка уведомлений { #notifications }

На локальном Sandbox возможно отлаживать отправку [уведомлений](notification.md) из задач.
Чтобы проверить отправку уведомлений по электронной почте, добавьте следующие настройки в `~/runtime_data/configs/settings.yaml`:

    ```yaml
    server:
      services:
        mailman:
          enabled: true
          whitelist: # Task types allowed to send e-mail notifications
             - MY_TEST_TASK
    ```

Проверить, что письма отправляются, можно в логе:

```bash
$ cat ~/runtime_data/logs/core/mailman.log
2019-01-16 09:52:12,937 DEBUG  (mailman) Waiting for 01m 00s
2019-01-16 09:53:13,357 INFO   (mailman) Sent 1, errors in 0 notification(s)
```

Следующие ошибки в логе, означают, что запущенный тип задачи не был добавлен в параметр `whitelist`:

```bash
$ cat ~/runtime_data/logs/core/mailman.log
2019-01-16 09:33:26,581 INFO   (mailman) Notification 5c3ed00cbf0cbc13d0b7f574 wasn't sent because of it isn't whitelisted.
2019-01-16 09:33:26,584 INFO   (mailman) Sent 1, errors in 0 notification(s)
```

## Разные настройки { #settings }

### Лимиты для процессов { #limits }

Если для процессов задачи нужно установить системные лимиты (`ulimit`), их можно указать в `/etc/security/limits.d/<your_login>.conf`, но с определёнными ограничениями:

* В первой колонке каждой строки нужно указывать логин, `*` не поддерживается.
* В значении лимита поддерживаются только целые числа, `unlimited` не поддерживается.

### Аутентификация в сторонних системах { #auth }

* Если задачи в локальном Sandbox требуют [SSH](https://en.wikipedia.org/wiki/SSH_(Secure_Shell)) ключи для аутентификации, то используются ключи из [SSH агента](https://en.wikipedia.org/wiki/Ssh-agent) и имя пользователя, запустившего Sandbox. Например, это нужно для работы с [Секретницей](https://yav.yandex-team.ru) и [секретами](secret.md).

    ```bash
    my-notebook $ ssh-agent
    my-notebook $ ssh-add ~/.ssh/id_rsa
    my-notebook $ ssh -A sandbox-test-vm.sas.yp-c.yandex.net # Ключ из ~/.ssh/id_rsa становится доступен на машине с Sandbox
    ```

    При использовании Секретницы необходимо делегировать секреты при помощи `curl`, используя хост и порт локального Sandbox:
    ```bash
    $ curl -X POST 'http://sandbox-test-vm.sas.yp-c.yandex.net:8000/api/v1.0/yav/tokens' -H 'Content-Type: application/json' -d '{"secrets": [{"id": "sec-***"}]}'
    ```

* Аутентификация в [Arcanum](https://a.yandex-team.ru/) API из задач использует токен из `~/oauth.token`.

### Звпуск задач использующих арк внутри lxc контейнеров { #arc_in_lxc }

1. Убедиться что в используемом контейнере установлен пакет fuse
2. Синхронизировать в локальный сандбокс ресурс типа ARC_CLIENT
