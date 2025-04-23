```
███╗   ███╗ ██████╗ ███╗   ██╗██╗████████╗ ██████╗ ██████╗ ██╗███╗   ██╗ ██████╗        █████╗ ███████╗       █████╗        ██████╗ ██████╗ ██████╗ ███████╗
████╗ ████║██╔═══██╗████╗  ██║██║╚══██╔══╝██╔═══██╗██╔══██╗██║████╗  ██║██╔════╝       ██╔══██╗██╔════╝      ██╔══██╗      ██╔════╝██╔═══██╗██╔══██╗██╔════╝
██╔████╔██║██║   ██║██╔██╗ ██║██║   ██║   ██║   ██║██████╔╝██║██╔██╗ ██║██║  ███╗█████╗███████║███████╗█████╗███████║█████╗██║     ██║   ██║██║  ██║█████╗
██║╚██╔╝██║██║   ██║██║╚██╗██║██║   ██║   ██║   ██║██╔══██╗██║██║╚██╗██║██║   ██║╚════╝██╔══██║╚════██║╚════╝██╔══██║╚════╝██║     ██║   ██║██║  ██║██╔══╝
██║ ╚═╝ ██║╚██████╔╝██║ ╚████║██║   ██║   ╚██████╔╝██║  ██║██║██║ ╚████║╚██████╔╝      ██║  ██║███████║      ██║  ██║      ╚██████╗╚██████╔╝██████╔╝███████╗
╚═╝     ╚═╝ ╚═════╝ ╚═╝  ╚═══╝╚═╝   ╚═╝    ╚═════╝ ╚═╝  ╚═╝╚═╝╚═╝  ╚═══╝ ╚═════╝       ╚═╝  ╚═╝╚══════╝      ╚═╝  ╚═╝       ╚═════╝ ╚═════╝ ╚═════╝ ╚══════╝

```

## Локальный запуск

Однократно:

```sh
$ make build
```

Пробный прогон:

```sh
$ make run -- --project paysys --environment stable -v --dry
```

При таком способе запуска пересобирать бинарь при каждом изменении не требуется (но нужны переменные окружения - см. ниже):

```sh
$ make run -- --project billing30 --environment stable --config tarifficator -v
```


## Как получить токены?
* Сonductor token: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=eb3c509c74b649cd8411ffc154543fe0
* Juggler token: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=cd178dcdc31a4ed79f42467f2d89b0d0
* Solomon token: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=1c0c37b3488143ff8ce570adb66b9dfa
* Yc token: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=8cdb2f6a0dca48398c6880312ee2f78d

Токены можно положить в `env.sh`, и перед запуском экспортировать переменные через `source env.sh`
```
export SOLOMON_TOKEN=***
export JUGGLER_TOKEN=***
export CONDUCTOR_TOKEN=***
export YC_TOKEN=***
```
Этот файл добавлен в `.arcignore`.


## Автоматический запуск

Для проекта можно так же дополнительно настроить автоматический запуск сборки и раскатки MaaC на PR и коммит в trunk.
Пример: [configs/balance_app/a.yaml](configs/balance_app/a.yaml).

Для создания аналогичного `a.yaml` для своего проекта можно воспользоваться `cookiecutter`:
```bash
$ pip3 install --user cookiecutter
$ make a.yaml
```

Потребуется ввести название директории проекта из `configs`, service slug и имя проекта.
Дополнительно потребуется выбрать токены робота, у которого есть доступ до ваших проектов в Juggler, Solomon и Conductor.
Для ускорения ввода они были сделаны выпадающим списком, поэтому добавить их можно прямо в [cookiecutter.json](templates/configs/a.yaml/cookiecutter.json).

## Документация
* Main concepts https://wiki.yandex-team.ru/dljaadminov/paysys/ps/monitorings-as-a-code/
* mczim's docs https://wiki.yandex-team.ru/DljaAdminov/paysys/Monitoring/
