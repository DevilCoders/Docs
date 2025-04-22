# Поддержка образов Docker

## Что уже готово {#done}

Поддержка в качестве среды исполнения программы образов собранных с помощью docker build. То есть layers из образа будут использоваться как layers в porto.

## Чего пока нет {#todo}

* Поддержка entrypoint'ов из Dockerfile (например CMD), вместо них используется instancectl (т.е. надо заполнять Instance Containers (services)).
* Поддержка переменных окружения, например ENV.
* Других опций/расширений из метаданных docker image.

## Ограничения на образ {#image-constraints}

* В образе должен быть доступен shell через `/bin/sh` (для работы iss хуков).

К образу должен иметь доступ (роль viewer) пользователь `robot-qloud-client`. [Инструкция](https://wiki.yandex-team.ru/cocaine/docker-registry-distribution/#upravlenieroljami) по добавлению роли.

## Использование своего образа {#custom-image}

Для добавления образа нужно перейти в раздел `Instance Spec` секции `Runtime`.
В поле `Instance type` выбрать `Docker Layers`.

![docker_service](https://jing.yandex-team.ru/files/sshipkov/dockerservice.875058c.png)

`Registry to use` устанавливается по умолчанию, можно поменять его на другой после согласования с командой nanny (нужен oauth token)
Формат имени образа описан [тут](https://docs.docker.com/engine/reference/run/#/imagetag). Поддерживается только нотация `Image:tag`, например `path/to/image:latest`.

## Порядок действий {#steps}

1. Сделать свой образ. Если в одном сервисе нужно будет запускать несколько команд, у каждого из которых ранее был свой докер-образ, то нужно собрать один образ, объединяющий все зависимости, которые требуют команды.
1. Дать доступ к своему образу пользователю `robot-qloud-client`.
1. Добавить образ в UI Nanny.

## Перенос способа запуска из Dockerfile {#migrate-cmd-from-dockerfile}

Если есть Dockerfile, с которым запуск команд уже работает, то перенос его на рельсы Nanny можно сделать одним из двух вариантов.

{% list tabs %}

- Вариант 1

  1. Перенести выставляемые переменные окружения из ENV в `Instance Spec 🠖 Instance Containers 🠖 Environment variables configuration`.
  1. Если далее эти переменные окружения передаются аргументами в команде, описанной в CMD, то передавать их как `{ENV_VAR}` вместо `$ENV_VAR`.

- Вариант 2

  1. Добавить в конец Dockerfile сохранение переменных среды, например `RUN bash -c -l "env | awk '{print \"export \" \$0;}' > export_vars.sh"`.
  1. В разделе Instance Spec добавить по одной секции `Instance Containers` на каждую CMD.
  1. В каждой CMD указать скрипт вида `/bin/bash -c "source /export_vars.sh && <command>"`, где `<command>` взята из CMD из Dockerfile.

{% endlist %}

## Обновление образа {#image-update}

Либо через выкатку нового снепшота (из-за любого изменения), либо через [Ticket Integration](docker-tickets-integration.md).

## tmpfs (чтобы выбранный дир был в памяти а не на винте) {#tmpfs}

Делается с помощью команды `portoctl vcreate /some_root_subdir backend=tmpfs space_limit=...e.g. 64M, 1G...'`, эту команду, скорее всего, разумно указать в Instance Spec 🠖 Instance Init Containers 🠖 Command.

{% note warning %}

Важно, что если смаунтить не в /корневую_папку, то всё отработает ок и даже df покажет, что tmpfs подмаунчена, **но по факту это будет hdd**. Проверить можно, например так: `F=/subdir/f ; time (cat /dev/zero | head -c30000000 > $F ; sync $F)`, 30Мб запишутся на hdd за сотни мс, а в память — за десятки мс.

{% endnote %}

## Где взять portoctl {#where-porto}

Бинарник portoctl входит в пакет yandex-porto и есть в стандартных образах нашего репозитория. Если же образ собран из внешних баз, то придется делать, например, так (вместо bionic, видимо, надо подставить требуемую версию ubuntu, например для debian buster подходит как раз bionic):

```bash
RUN echo 'deb http://dist.yandex.ru/search-bionic/ stable/amd64/ \n\
deb http://dist.yandex.ru/search-bionic/ stable/all/ \n\
deb http://dist.yandex.ru/search-bionic/ unstable/amd64/ \n\
deb http://dist.yandex.ru/search-bionic/ unstable/all/' \
    >> /etc/apt/sources.list \
    && (apt \
        -o Acquire::AllowInsecureRepositories=true \
        -o Acquire::AllowDowngradeToInsecureRepositories=true \
        update \
    || :) \
    && apt-get \
        install \
        -y \
        --allow-unauthenticated \
        yandex-porto \
    && rm -rf /var/lib/apt/lists/*
```
В команде выше обходятся проблемы с секьюрностью реп и игнорируются ошибки.

## Особенности реализации {#implementation}

* Пользователь, от которого запущено всё – `root`.
* Cwd на хосте – `/db/iss3/instances/<instance_id>`
Директория /db/iss3/instances/<instance_id> биндится в контейнер, собранный на базе образа docker. Хуки iss запускаются из нее, все ресурсы, используемые сервисом (точнее, ссылки на них) находятся там же.
Если нужно позвать внешний бинарь из образа, путь к нему не будет зависеть от instance_id:

```
/bin/sleep 1000
```
* Сеть остаётся хостовой, поэтому надо слушать нужный порт $BSCONFIG_IPORT или %(annotated_ports_n)s.

