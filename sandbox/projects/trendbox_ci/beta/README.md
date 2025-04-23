# Trendbox CI. Sandbox Cloud Tasks (dist tag: beta)

Код [Sandbox-задачи][sandbox-tasks] `TRENDBOX_CI_JOB_BETA`.

[sandbox]: https://wiki.yandex-team.ru/sandbox/
[sandbox-tasks]: https://wiki.yandex-team.ru/sandbox/tasks/

## Содержание

* [Разработка](#разработка)
  * [Исходный код](#исходный-код)
  * [Настройка](#настройка)
  * [Сборка](#сборка)
  * [Отладка](#отладка)
  * [Запуск тестов](#запуск-тестов)
  * [Code Style](#code-Style)
* [Релизы](#релизы)

## Разработка

### Настройка

Для удобства работы с Sandbox-инструментами необходимо добавить [OAuth]-токен в файл `~/.sandbox/<login>.oauth`.

Получить свой OAuth-токен можно по [ссылке](https://sandbox.yandex-team.ru/oauth).

### Сборка

Чтобы собрать код задач используйте утилиту [ya].

```console
$ cd acradia/sandbox/projects/trendbox_ci/beta/bin/
$ ya make
```

> 📖 Подробнее о сборке Sandbox-задач читайте в [документации][sandbox-build].
>
> :warning: Чтобы использовать бинарный файл в [production][sandbox-production]-окружении Sandbox, он должен быть собран на `Linux`-машине ([SANDBOX-6799]).

После сборки в директории `bin` появится утилита с названием `trendbox_ci`.

```console
$ cd arcadia/sandbox/projects/trendbox_ci/beta/bin
$ ./trendbox_ci --help

usage: v0 [-h] <command> ...

Tasks binary.

optional arguments:
  -h, --help  show this help message and exit

subcommands:
  <command>   <description>
    run       Subcommand to run task.
    upload    Binary uploading subcommand.
    content   Binary content analysis.
    ipython   Run ipython using built tasks code.
    interpret
              Interpret given script using built environment.
```

### Отладка

После сборки, создайте Sandbox-задачу из собранного кода.

```console
$ cd arcadia/sandbox/projects/trendbox_ci/beta/bin
$ ./trendbox_ci run --create-only --type TRENDBOX_CI_JOB_BETA

...
2022-01-19 15:46:04 INFO Task of type TRENDBOX_CI_JOB_BETA created: https://sandbox.yandex-team.ru/task/1188535807
...
```

#### Отладка server-side кода

Чтобы проверить изменения в параметрах или требованиях SB-задачи, используйте опцию `--enable-taskbox`.

```console
$ cd arcadia/sandbox/projects/trendbox_ci/beta/bin
$ ./trendbox_ci run --create-only --enable-taskbox --type TRENDBOX_CI_JOB_BETA
```

Созданная задача будет содержать изменения в параметрах или требованиях.

> :warning: На данный момент работа `--enable-taskbox` нестабильна. Нет возможности запустить Sandbox-задачу через Sandbox UI.

Чтобы запустить задачу с изменёнными параметрами или требованиями, передайте их в JSON-формате.

```console
$ cd arcadia/sandbox/projects/trendbox_ci/beta/bin
$ ./trendbox_ci run --enable-taskbox --type TRENDBOX_CI_JOB_BETA '{ "custom_fields": [{ "name": "string", "value": {} }], "requirements": {} }'
```

### Запуск тестов

Чтобы запустить тесты задач используйте утилиту [ya].

```console
$ cd arcadia/sandbox/projects/trendbox_ci/beta
$ ya make -tt
```

Чтобы проверить бинарную сборку задач, запустите тесты для всех Sandbox-задач.

```console
$ cd arcadia
$ ya make -tt --dist sandbox/tasks/tests
```

### Code Style

Проверка стиля выполняется при запуске тестов, как и для любого другого python-кода в Аркадии. Подробнее о требованиях предъявляемых к Python-коду Аркадии читайте в [style guide][python_style_guide].

Для Sandbox-задач [включена][sandbox_flake8] проверка с помощью `flake8`. Подробнее читайте в [посте][arcadia_flake_8].

[python_style_guide]: https://docs.yandex-team.ru/arcadia-python/python_style_guide
[arcadia_flake_8]: https://clubs.at.yandex-team.ru/arcadia/21095
[sandbox_flake8]: https://a.yandex-team.ru/arc_vcs/sandbox/pytest.ini?rev=d0928c34e691723b6be71a407e0d762e23cfb76e#L2

## Релизы

Изменения попадут в продакшен окружение Sandbox-задач через некоторое время после влития в `trunk`.

В CI настроены [релизы][releases] кода задач. После влития пулл-реквеста будет запущена сборка Sandbox-ресурса с типом [SANDBOX_TASKS_BINARY]. Ресурс будет зарелижен в `prestable` и использоваться при тестировании сервисов Trendbox CI в пулл-реквестах.

> Подробнее об использовании кода задач в продакшен читайте в [релизной документации](https://github.yandex-team.ru/search-interfaces/trendbox-ci/blob/master/docs/devops/release.md) к Trendbox CI.

[ci]: https://a.yandex-team.ru/arc/trunk/arcadia/ci#разработка-ci
[oauth]: https://wiki.yandex-team.ru/intranet/dev/oauth/
[ya]: https://wiki.yandex-team.ru/yatool/
[trunk]: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/trendbox_ci/beta/
[sandbox]: https://wiki.yandex-team.ru/sandbox/
[sandbox-build]: https://wiki.yandex-team.ru/sandbox/tasks/build/
[sandbox-production]: https://wiki.yandex-team.ru/sandbox/tasks/build/
[sandbox-binary-restrictions]: https://wiki.yandex-team.ru/sandbox/tasks/binary/#restrictions
[SANDBOX-6799]: https://st.yandex-team.ru/SANDBOX-6799
[SANDBOX_TASKS_BINARY]: https://sandbox.yandex-team.ru/resources?type=SANDBOX_TASKS_BINARY&owner=TRENDBOX_CI_TEAM&state=READY&limit=20&attrs=%7B%22project%22%3A%22trendbox_ci%22%2C%22project_dist_tag%22%3A%22beta%22%2C%22released%22%3A%22prestable%22%7D
[releases]: https://a.yandex-team.ru/projects/trendbox-ci/ci/releases/timeline?dir=sandbox%2Fprojects%2Ftrendbox_ci%2Fbeta&id=release_sandbox_tasks