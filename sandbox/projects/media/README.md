### Бинарные задачи
Бинарные задачи позволяют тестировать код в продакшн sandbox'е без коммита
Для создания бинарной задачи:
  * Директория с ней должна быть CamelCase
  * Класс задачи должен иметь аттрибут `BINARY_TASK_ATTR_TARGET = "<path_from_bin.sh>"`
  * Класс задачи должен иметь блок параметров для выбора релизного типа бинарной задачи:
```python
    with sdk2.parameters.Group("Task resource settings", collapse=True) as build_settings_block:
        UseLastBinary = sdk2.parameters.Bool("Use last binary archive", default=True)
        with UseLastBinary.value[True]:
            with sdk2.parameters.RadioGroup("Binary release type") as ReleaseType:
                ReleaseType.values.stable = ReleaseType.Value("stable", default=True)
                ReleaseType.values.test = ReleaseType.Value("test")
        with UseLastBinary.value[False]:
            custom_tasks_archive_resource = sdk2.parameters.Resource("task archive resource", default=None)
```
  * Класс задачи должен иметь метод `on_save` (by default при создании задачи в sandbox - будет создаваться бинарная stable задача):
```python
def on_save(self):
    if self.Parameters.UseLastBinary:
        self.Requirements.tasks_resource = sdk2.service_resources.SandboxTasksBinary.find(
            attrs={"target": self.BINARY_TASK_ATTR_TARGET,
                   "release": self.Parameters.ReleaseType or "stable"}
        ).first().id
    else:
        self.Requirements.tasks_resource = self.Parameters.custom_tasks_archive_resource
```
  * В директории задачи должна быть директория `bin` с `ya.make` вида:
```yamake
SANDBOX_TASK(platformcheckcerts-runner)
OWNER(
    g:kp-sre
    g:afisha-sre
)
PEERDIR(
    sandbox/projects/media/admins/PlatformCheckCerts
)
END()
```

#### Сборка и релиз бинарной задачи
Для упрощенной работы написан `./bin.sh`: достаточно передать ему путь до директории с задачей и тип релиза (дефолт: `test`)

e.g.: `./bin.sh admins/PlatformCheckCerts stable`
