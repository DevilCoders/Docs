# ya project
MJ интегрирован в команды создания/обновления исходного кода [ya project create/update](https://docs.yandex-team.ru/ya-make/usage/ya_project). Это значит, что с помощью команд ya project можно создавать сервисы на MJ и проводить в них регенерацию.

## ya project create MJ
С помощью команды `ya project create MJ` можно создать сервис на MJ. 

Команда принимает на вход различные аргументы, о которых можно узнать выполнив команду с аргументом `-- --help` (тут нет опечатки, сначала `--`, потом `--help`)

```
$ ya project create MJ -- --help
usage: ya project create MJ [destination_path] [-h] -n NAME -p PACKAGE -o
                                               YA_OWNER -m TRACE_MODULE -u
                                               AUTHOR [-r {nanny,deploy}]

Create MJ project. Destination directory must not exist or to be empty

optional arguments:
  -h, --help            show this help message and exit
  -n NAME, --name NAME  application name
  -p PACKAGE, --package PACKAGE
                        java package. For example:
                        ru.yandex.market.team.application
  -o YA_OWNER, --ya-owner YA_OWNER
                        ya make owner. For example: g:marketinfra
  -m TRACE_MODULE, --trace-module TRACE_MODULE
                        trace module. For example: TSUM_API
  -u AUTHOR, --author AUTHOR
                        service author. For example: sid-hugo
  -r {nanny,deploy}, --deploy-type {nanny,deploy}
                        deploy type. Must be one of: 'nanny' or 'deploy'
```

**Пример**
```
ya project create MJ market/infra/my_best_service -n my_service -p ru.yandex.market.team.application -o g:marketdevexp -m MY_MODULE -u sid-hugo -r deploy
```

После выполнения  команды:
- будет создан код сервиса в папке `market/infra/my_best_service` (путь относительно текущей папки)
- в `service.yaml` в `java_service.service_name` будет указано имя сервиса `my_service`
- в `service.yaml` в `java_service.root_package` будет указан пакет `ru.yandex.market.team.application`
- в `service.yaml` в `trace.module` будет прописано `MY_MODULE`
- в `package.json` в поле `maintainer` будет прописано `sid-hugo`
- в `ya.make` в поле `OWNER` будет прописано `g:marketdevexp`
- `package.json` будет написан так, чтобы сервис корректно разворачивался в `yandex deploy`

## ya project update MJ
С помощью команды `ya project update MJ` можно произвести регенерацию сервиса на MJ. О том, когда производить регенерацию, можно узнать [здесь](how_it_works/about.md). 

Команда принимает на вход различные аргументы, о которых можно узнать выполнив команду с аргументом `-- --help` (тут нет опечатки, сначала `--`, потом `--help`)
```
$ ya project update MJ -- --help
usage: ya project update MJ [-h] [-i IDEA] [-g GENERATION_FOLDER] [-novcs]
                            [-ideflags [IDE_FLAGS [IDE_FLAGS ...]]] [-withide]

Regenerate MJ project

optional arguments:
  -h, --help            show this help message and exit
  -i IDEA, --idea IDEA  directory for idea project
  -g GENERATION_FOLDER, --generation_folder GENERATION_FOLDER
                        local arcadia path
  -novcs                do not add templates to vcs
  -ideflags [IDE_FLAGS [IDE_FLAGS ...]], --ide_flags [IDE_FLAGS [IDE_FLAGS ...]]
                        additional flags for ya ide idea
  -withide, --with_ya_ide
                        enable ya ide idea command

```

Команда поддерживает все опции генерации, описанные [здесь](features/generation_settings.md).

{% note warning %}

По умолчанию, команда `ya project update MJ` не вызывает команду `ya ide idea` и не создает проект для IDEA. Как следствие, так же не создаются Run Configurations.

Сделано это из-за того, что семейство команд `ya project` отвечают за исходный код, а семейство команд `ya ide` за создание проекта для IDE. 

Но если вызывать `ya ide idea` все таки очень хочется, имеется флаг `-withide` или `--with_ya_ide`.

{% endnote %}
