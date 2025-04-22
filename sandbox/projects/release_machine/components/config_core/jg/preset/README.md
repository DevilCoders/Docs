# Пресеты JG

Пресеты секции `JG` конфигов компонент RM. Живут в [sandbox/projects/release_machine/components/config_core/jg/preset](https://a.yandex-team.ru/arcadia/sandbox/projects/release_machine/components/config_core/jg/preset). Каждый такой пресет определяет параметризованный некоторым образом граф (или даже несколько графов), который(-ые) можно уточнять/менять/расширять.

**Зачем это нужно?**

Чтобы упростить всем жизнь. К примеру, огромное количество компонент Релизной машины имеют релизные циклы вида "_отвести ветку/тег -> собрать цель -> зарелизить цель_" (ну и + всякие обвязки от RM — changelog'и, тикеты и т.п.). Довольно бессмысленно описывать всякий раз такой граф заново в каждой компоненте: отличаются все эти графы лишь целью сборки, сервисами (куда катить) и еще, возможно, несколькими настройками. Пресет JG позволяет по набору параметров получить готовый граф известного вида

## Использование

Использование того или иного пресета сводится к наследованию секции `JG` своего конфига от класса соответствующего пресета. Например:

```python

from sandbox.projects.release_machine.components import configs
from sandbox.projects.release_machine.components.config_core.jg.preset import basic_build_presets

class MyShinyConfig(configs.ReferenceCIConfig):

    # <some settings>

    class JG(basic_build_presets.SingleBuildYaMakeJGCfg):
        pass

    # <some other settings>

```

Пресеты могут иметь необходимые или опциональные параметры, которые вводятся через атрибуты и методы класса. Подробности о каждом отдельном пресете можно найти ниже

## Релизные пресеты

Пресеты релизных графов — то есть, тех, которые запускаются в релизных ветках. Базовый класс JG — BaseReleaseMachineJobGraph — определяет internal-подграф релизного графа (технические кубики RM) и базовую структуру самого релизного графа (метод release).  Релизные пресеты расширяют этот базовый релизный граф, добавляя в него кубики сборки, релиза и прочие.

### SingleBuildGeneralJGCfg { #SingleBuildGeneralJGCfg }

[[source](https://a.yandex-team.ru/svn/trunk/arcadia/sandbox/projects/release_machine/components/config_core/jg/preset/basic_build_presets.py)]

Один сборочный кубик и несколько релизных. Опционально также может подниматься Yappy-бета.

Схема графа (опциональные кубики обрамлены пунктирной линией)

%%(graphviz)
digraph SingleBuildGeneralJGCfg {

    graph [rankdir="LR"]

    NewTag [shape=rect]
    MainGraphEntry [fontsize=6]
    Build [shape=rect]
    GenerateYappyBeta [shape=rect, style=dashed]
    Release1 [shape=rect]
    Release2 [shape=rect]
    CreateChangelog [shape=rect]
    CreateStartrekTicket [shape=rect, style=dashed]
    FormatChangelog [shape=rect]
    LinkFeatureTickets [shape=rect, style=dashed]
    PostChangelogToStartrek [shape=rect, style=dashed]
    CreateWikiPageWithChangelog [shape=rect, style=dashed]
    TestStageEntry [fontsize=6, style=dashed]
    ReleaseStageEntry [fontsize=6]

    NewTag -> MainGraphEntry

    MainGraphEntry -> CreateChangelog
    MainGraphEntry -> CreateStartrekTicket
    MainGraphEntry -> Build
    CreateChangelog -> FormatChangelog
    CreateStartrekTicket -> PostChangelogToStartrek
    CreateStartrekTicket -> LinkFeatureTickets
    CreateChangelog -> LinkFeatureTickets
    FormatChangelog -> PostChangelogToStartrek
    CreateStartrekTicket -> CreateWikiPageWithChangelog
    CreateChangelog -> CreateWikiPageWithChangelog


    LinkFeatureTickets -> TestStageEntry
    CreateWikiPageWithChangelog -> TestStageEntry
    PostChangelogToStartrek -> TestStageEntry
    Build -> TestStageEntry

    TestStageEntry -> GenerateYappyBeta

    GenerateYappyBeta -> ReleaseStageEntry

    ReleaseStageEntry -> Release1
    ReleaseStageEntry -> Release2
}
%%

Это базовый класс для других аналогичных пресетов: в нем не определен билд. Тем не менее, его можно использовать в пользовательских конфигах в случаях, когда граф включает сугубо кастомный билд (в таком случае необходимо доопределить в своем JG атрибут `build_task` и метод `_get_build_cube`).

Пример использования: [begemot_megamind](https://a.yandex-team.ru/arc_vcs/sandbox/projects/release_machine/components/configs/alice/begemot/begemot_megamind.py?rev=r9772371#L140)

### SingleBuildYaMakeJGCfg { #SingleBuildYaMakeJGCfg }

[[source](https://a.yandex-team.ru/svn/trunk/arcadia/sandbox/projects/release_machine/components/config_core/jg/preset/basic_build_presets.py)]

Один сборочный кубик и несколько релизных. Опционально также может подниматься yappy-бета. Граф — как и в `SingleBuildGeneralJGCfg`. Кубик `build` запускает Sandbox-задачу **YA_MAKE_2**.

Пути сборки и направления релиза вычисляются по настройке `ReleasesCfg.releasable_items`. В релиз с этим пресетом попадут лишь те releasable item-ы, для которых определены тип Sandbox-ресурсы (параметр `data`), путь сборки (параметр `build_data`) и заполнена информация о выкатке (параметр `deploy_infos`). Пример:

```python
    class Releases(configs.ReferenceCIConfig.Releases):
        @property
        def releasable_items(self):
            return [
                configs.ri.ReleasableItem(
                    name="my_shiny_releasable_item",
                    build_data=configs.ri.BuildData(
                        target="path/to/my/target",
                        artifact="path/to/my/target/bin_name",
                    ),
                    data=configs.ri.SandboxResourceData("MY_TARGET_RESOURCE"),
                    deploy_infos=[
                        configs.ri.single_nanny_service("my_nanny_service"),
                    ],
                ),
            ]
```

### SingleBuildKosherYaMakeJGCfg { #SingleBuildKosherYaMakeJGCfg }

[[source](https://a.yandex-team.ru/svn/trunk/arcadia/sandbox/projects/release_machine/components/config_core/jg/preset/basic_build_presets.py)]

Один сборочный кубик и несколько релизных. Опционально также может подниматься yappy-бета. Граф — как и в `SingleBuildGeneralJGCfg`. Кубик `build` запускает Sandbox-задачу **KOSHER_YA_MAKE** (наследник **YA_MAKE_2** с плюшками и хуком для релиза в няню).

Пути сборки и направления релиза вычисляются по настройке `ReleasesCfg.releasable_items`. В релиз с этим пресетом попадут лишь те releasable item-ы, для которых определены тип Sandbox-ресурсы (параметр `data`), путь сборки (параметр `build_data`) и заполнена информация о выкатке (параметр `deploy_infos`). Пример:

```python
    class Releases(configs.ReferenceCIConfig.Releases):
        @property
        def releasable_items(self):
            return [
                configs.ri.ReleasableItem(
                    name="my_shiny_releasable_item",
                    build_data=configs.ri.BuildData(
                        target="path/to/my/target",
                        artifact="path/to/my/target/bin_name",
                    ),
                    data=configs.ri.SandboxResourceData("MY_TARGET_RESOURCE"),
                    deploy_infos=[
                        configs.ri.single_nanny_service("my_nanny_service"),
                    ],
                ),
            ]
```


### SingleBuildYaMakeTemplateJGCfg { #SingleBuildYaMakeTemplateJGCfg }

[[source](https://a.yandex-team.ru/svn/trunk/arcadia/sandbox/projects/release_machine/components/config_core/jg/preset/basic_build_presets.py)]

То же, что и SingleBuildYaMakeJGCfg, только в качестве сборочной задачи предполагается кастомный наследник [YaMakeTemplate](https://a.yandex-team.ru/arc_vcs/sandbox/projects/common/build/tasks/YaMakeTemplate/__init__.py). Использование этого пресета предполагает переопределение атрибута `build_task`:

```python
    class JG(basic_build_presets.SingleBuildYaMakeTemplateJGCfg):
        build_task = "MY_CUSTOM_BUILD_TASK"
        ...
```

### SingleBuildYaPackageJGCfg { #SingleBuildYaPackageJGCfg }

[[source](https://a.yandex-team.ru/svn/trunk/arcadia/sandbox/projects/release_machine/components/config_core/jg/preset/basic_build_presets.py)]

То же, что и SingleBuildYaMakeJGCfg, только в качестве сборочной задачи используется YA_PACKAGE_2. В `build_data` релизных айтемов при этом нет необходимости указывать `artifacts`.


### SingleBuildYaPackageInheritorJGCfg { #SingleBuildYaPackageInheritorJGCfg }

[[source](https://a.yandex-team.ru/svn/trunk/arcadia/sandbox/projects/release_machine/components/config_core/jg/preset/basic_build_presets.py)]

То же, что и SingleBuildYaPackageJGCfg, но в качестве сборочной задачи используется наследник YaPackage(2). Использование этого пресета предполагает переопределение атрибута `build_task`:

```python
    class JG(basic_build_presets.SingleBuildYaPackageInheritorJGCfg):
        build_task = "MY_CUSTOM_YA_PACKAGE"
        ...
```

### TaskletBuildPreset { #TaskletBuildPreset }

[[source](https://a.yandex-team.ru/svn/trunk/arcadia/sandbox/projects/release_machine/components/config_core/jg/preset/basic_build_presets.py)]

Пресет для релиза тасклетов

#### Пример

[Пример конфига](https://a.yandex-team.ru/arc//trunk/arcadia/sandbox/projects/release_machine/components/configs/rm_tasklet_bundle.py)

#### Настройки

Секция `Releases` должна иметь следующий вид:

```python
class Releases(configs.ReferenceCIConfig.Releases):
    @property
    def releasable_items(self):
        return [
            configs.ri.ReleasableItem(
                name="some_name",
                data=configs.ri.SandboxResourceData("SANDBOX_TASKS_BINARY", ttl=14),
                build_data=configs.ri.BuildData(
                    target="path/to/my/tasklet/directory",
                    artifact="path/tomy/tasklet/directory/binary",
                ),
                deploy_infos=[
                    configs.ri.CiTaskletRegistryDeployInfo(
                        registry_paths=[
                            "tasklet/registry/path1",
                            "tasklet/registry/path2",
                            "tasklet/registry/path3",
                            "tasklet/registry/pathN",
                        ],
                    ),
                ]
            ),
        ]
```

**Важно**:

- releasable item должен быть только один. Если хочется релизить сразу несколько тасклетов, собираем все в один ya.make ([пример](https://a.yandex-team.ru/arc_vcs/release_machine/tasklets/bundle)) и собираем именно его
- в `build_data` target — это путь до папки, а artifact — до бинаря (иными словами, типичным образом  artifact == "{target}/{binary_name}")
- в `registry_paths` должны быть перечислены **все** пути в реестре, в которые хочется релизить (<=> коммитить новые версии)
- пути в `registry_paths` указываются относительно `ci/registry` и **без** суффикса ".yaml" (например, `"projects/release_machine/commit_tasklet_version"`)


В `JG` можно также добавить параметр `release_ticket`:

```python
class JG(basic_build_presets.TaskletBuildPreset):
    release_ticket = "WHATEVER-111"
```

Тогда все коммиты с обновлением версий тасклетов будут линковаться к этому тикету. Само собой, настройка может содержать и JMESPath — например, для доступа к контексту или выхлопу других кубиков


### ApphostVerticalJGCfg { #ApphostVerticalJGCfg }

[[source](https://a.yandex-team.ru/svn/trunk/arcadia/sandbox/projects/release_machine/components/config_core/jg/preset/apphost_vertical_presets.py)]

Пресет релизов аппхостовых вертикалей
