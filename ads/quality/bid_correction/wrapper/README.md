# wrapper
Утилита для запуска бинарника `workflow_constructor`.
Использование: `./wrapper <режим> <аргументы workflow_constructor>`.
Имеет два режима:
- `run` - запустить бинарь с аргументами.
По умолчанию запускается последний stable-ресурс с sandbox.
Можно указать свой бинарь опцией `--local_stable_workflow_constructor_binary` или ID ресурса на Sandbox опцией `--local_stable_workflow_constructor_resource_id`.
- `diff` - посчитать дифф между графами, построенными двумя версиями workflow_constructor: stable и собранной локально.
Stable-версия аналогична режиму `run`, локальная версия по умолчанию берется из `arcadia/ads/quality/bid_correction/workflow_constructor/workflow_constructor`
(можно переопределить опцией `--workflow_constructor_binary`).
Результат сохраняется в файл `diff.html` (можно переопределить опцией `-o/--output`).
