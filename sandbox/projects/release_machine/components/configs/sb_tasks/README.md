## Релизные машины для бинарных задач Sandbox

RM over CI конфиг для релиза бинарной задачи пишется в нескольких строк при  использовании пресета `SandboxSingleTaskReleaseCfg`. Этот пресет определяет граф, состоящий из технических кубиков RM (new tag, changelog и т.п.), сборки и релиза бинаря задачи. Опционально можно включить релиз в тестинг с последующим запуском задачи с заданными параметрами — своего рода приемка. О пресете можно почитать также в его собственном докстринге.

Работает на [RM over CI](https://wiki.yandex-team.ru/releasemachine/rm-over-ci/). a.yaml будет создан в папке задачи.

### Дефолты

Пресет `SandboxSingleTaskReleaseCfg` подразумевает следующую структуру кода задачи:

- `/sandbox/projects/some/path/MyTask` — путь до кода Sandbox-задачи (PY23_LIBRARY/PY_LIBRARY). Сюда будет записан a.yaml
- `/sandbox/projects/some/path/MyTask/bin` — таргет сборки (SANDBOX_TASK/SANDBOX_PY3_TASK) — этот путь необходимо явно задать в конфиге
- вычисляется по пути до задачи (например, `"MY_TASK"`)
- имя бинаря совпадает с типом таски в нижнем регистре snake_case
- (в случае добавления запуска задачи) описание в реестре CI живет по пути `projects/{responsible_abc_service_name}/{target_task_type_lowercase}.yaml`

При необходимости все это можно настраивать в конфиге:
- `target_task_path`
- `target_task_path_no_bin`
- `target_task_type`
- `target_bin_name`
- `target_task_ci_registry_location`

### Конфиг

#### Минимальный конфиг

Технические кубики + сборка + релиз в стейбл

Все, что нужно определить — имя компоненты, abc-сервис, дефолтного ответственного, путь до задачи и Sandbox-группу

```python
# -*- coding: utf-8 -*-
from sandbox.projects.release_machine.components import configs
from sandbox.projects.release_machine.components.configs.sb_tasks import _base as sb_cfg_base


class MyTaskCfg(sb_cfg_base.SandboxSingleTaskReleaseCfg):
    name = "my_task"
    responsible = configs.Responsible(
        abc=configs.Abc(service_name="my_service"),
        login="default_responsible_user",
    )
    target_task_path = "sandbox/projects/path/to/my/task/bin"

    class CI(sb_cfg_base.SandboxSingleTaskReleaseCfg.CI):
        sb_owner_group = "MY_SANDBOX_GROUP"

```

#### Дополнительные атрибуты

Если нужно раздать ресурсу дополнительных атрибутов, это можно сделать так

```python
# -*- coding: utf-8 -*-
from sandbox.projects.release_machine.components import configs
from sandbox.projects.release_machine.components.configs.sb_tasks import _base as sb_cfg_base


class MyTaskCfg(sb_cfg_base.SandboxSingleTaskReleaseCfg):
    name = "my_task"
    responsible = configs.Responsible(
        abc=configs.Abc(service_name="my_service"),
        login="default_responsible_user",
    )
    target_task_path = "sandbox/projects/path/to/my/task/bin"

    @property
    def task_binary_resource_additional_attributes(self):
        return {
            "some_key": "some_value",
        }

    class CI(sb_cfg_base.SandboxSingleTaskReleaseCfg.CI):
        sb_owner_group = "MY_SANDBOX_GROUP"

```

#### Конфиг с тестовым запуском

Технические кубики + сборка + релиз в тестинг + запуск из тестинга на заданных параметрах + релиз в стейбл

Добавляется описание инпута для тестового запуска

```python
# -*- coding: utf-8 -*-
from sandbox.projects.release_machine.components import configs
from sandbox.projects.release_machine.components.configs.sb_tasks import _base as sb_cfg_base
from sandbox.projects.release_machine.components.config_core.jg import cube as jg_cube


class MyTaskCfg(sb_cfg_base.SandboxSingleTaskReleaseCfg):
    name = "my_task"
    responsible = configs.Responsible(
        abc=configs.Abc(service_name="my_service"),
        login="default_responsible_user",
    )
    target_task_path = "sandbox/projects/path/to/my/task/bin"

    @property
    def test_run_input(self):
        return jg_cube.CubeInput(
            my_custom_param_1="my_custom_value_1",
            my_custom_param_2="my_custom_value_2",
            my_custom_param_3="my_custom_value_3",
        )

    class CI(sb_cfg_base.SandboxSingleTaskReleaseCfg.CI):
        sb_owner_group = "RELEASE_MACHINE"

```

Для работы тестового запуска необходимо, чтобы задача была [зарегистрирована в реестре CI](https://docs.yandex-team.ru/ci/job-sandbox).
По умолчанию подразумевается, что соответствующее описание лежит по пути `projects/{responsible_abc_service_name}/{target_task_type_lowercase}.yaml`.
Можно указать произвольный путь с помощью опции `target_task_ci_registry_location`.

Пример YAML с описанием Sandbox-задачи:

```yaml
title: MySandboxTask
description: MySandboxTask Description
maintainers: <responsible_abc_service_name>

sandbox-task:
  name: MY_SANDBOX_TASK
```

Подробности: https://docs.yandex-team.ru/ci/job-sandbox

Над автоматической генерацией YAML-описаний для таких задач думаем в [RMDEV-3272](https://st.yandex-team.ru/RMDEV-3272)

#### Конфиг с тестовым запуском и прекоммитной проверкой

Все то же, только добавляется флоу, который будет запускаться на PR в папку с задачей

Добавляется параметр `add_precommit_check = True`

**Требует регистрации задачи в реестре CI** (см. выше "Конфиг с тестовым запуском")

```python
# -*- coding: utf-8 -*-
from sandbox.projects.release_machine.components import configs
from sandbox.projects.release_machine.components.configs.sb_tasks import _base as sb_cfg_base
from sandbox.projects.release_machine.components.config_core.jg import cube as jg_cube


class MyTaskCfg(sb_cfg_base.SandboxSingleTaskReleaseCfg):
    name = "my_task"
    responsible = configs.Responsible(
        abc=configs.Abc(service_name="my_service"),
        login="default_responsible_user",
    )
    target_task_path = "sandbox/projects/path/to/my/task/bin"

    add_precommit_check = True

    @property
    def test_run_input(self):
        return jg_cube.CubeInput(
            my_custom_param_1="my_custom_value_1",
            my_custom_param_2="my_custom_value_2",
            my_custom_param_3="my_custom_value_3",
        )

    class CI(sb_cfg_base.SandboxSingleTaskReleaseCfg.CI):
        sb_owner_group = "RELEASE_MACHINE"

```



#### Релиз в stable по кнопке


```python
# -*- coding: utf-8 -*-
from sandbox.projects.release_machine.components import configs
from sandbox.projects.release_machine.components.configs.sb_tasks import _base as sb_cfg_base


class MyTaskCfg(sb_cfg_base.SandboxSingleTaskReleaseCfg):
    name = "my_task"
    responsible = configs.Responsible(
        abc=configs.Abc(service_name="my_service"),
        login="default_responsible_user",
    )
    target_task_path = "sandbox/projects/path/to/my/task/bin"

    release_to_stable_manually = True

    class CI(sb_cfg_base.SandboxSingleTaskReleaseCfg.CI):
        sb_owner_group = "MY_SANDBOX_GROUP"

```

### Примеры

#### LaunchMetrics

- [Конфиг](https://a.yandex-team.ru/arc_vcs/sandbox/projects/release_machine/components/configs/sb_tasks/launch_metrics.py)
- [a.yaml](https://a.yandex-team.ru/arc_vcs/sandbox/projects/release_machine/tasks/LaunchMetrics/a.yaml)
- [Страница в RM](https://rm.z.yandex-team.ru/component/launch_metrics/manage2?action_id=release_launch_metrics)
- [Страница в CI](https://a.yandex-team.ru/projects/releasemachine/ci/releases/timeline?dir=sandbox/projects/release_machine/tasks/LaunchMetrics&id=release_launch_metrics)

#### PrepareCiEnvironment

- [Конфиг](https://a.yandex-team.ru/arc_vcs/sandbox/projects/release_machine/components/configs/sb_tasks/prepare_ci_environment.py)
- [a.yaml](https://a.yandex-team.ru/arc_vcs/sandbox/projects/release_machine/tasks/PrepareCiEnvironment/a.yaml)
- [Страница в RM](https://rm.z.yandex-team.ru/component/prepare_ci_environment/manage2?action_id=release_prepare_ci_environment)
- [Страница в CI](https://a.yandex-team.ru/projects/releasemachine/ci/releases/timeline?dir=sandbox/projects/release_machine/tasks/PrepareCiEnvironment&id=release_prepare_ci_environment)
