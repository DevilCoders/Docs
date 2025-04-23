# dcsaap-python

Специальная сборка python3 с требуемыми библиотеками для запуска небольших скриптов проекта в Nirvana без компиляции.

## Используемые библиотки

- `contrib/python/requests`: для выполнения HTTP-запросов
- `yql/library/python`: для запуска YQL в скриптах

## Использование в Nirvana

### Добавление приложения в операцию

Добавление приложения в операцию осуществляется через [добавление ресурса](https://wiki.yandex-team.ru/nirvana/manual/create_operation/#resources).

#### Через Sandbox
Для того, чтобы не загружать ресурс вручную, можно воспользоваться вкладкой `Sandbox` добаляемого ресурса:
- `Target path in Arcadia`: `billing/dcsaap/nirvana/python`
- `Artifact path`: `billing/dcsaap/nirvana/python/dcsaap-python`
- `Type`: `Executable`
- `Resource name`: `dcsaap-python`

После нажатия `Upload` Nirvana создаст Sandbox-задачу, после выполнения которой `dcsaap-python` автоматически будет загружен как ресурс операции. Запущенную Sandbox-задачу можно найти с помощью [фильтра](https://sandbox.yandex-team.ru/tasks?author=robot-nirvana&desc_re=Stored&type=YA_MAKE&limit=20).

#### Вручную
Для ручной загрузки ресурса используется вкладка `Local file`. Файл компилируется на машине разработчика (`ya make`) и загружается через интерфейс Nirvana.


### Использование приложения в операции

Для использования ресурса Nirvana предоставляет шаблонный синтаксис `${resource["dcsaap-python"]}`, который можно использовать для запуска приложения.

В связи с тем, что `dcsaap-python` на самом деле является `IPython`-приложением, для передачи агрументов в запускаемый скрипт их требуется отделить через `--`.

Примеры:
- Запуск скрипта, переданного через Input:
```bash
${resource["dcsaap-python"]} ${input["input"]}
```
- Запуск скрипта с выводом в Output:
```bash
bash -c "${resource["dcsaap-python"]} ${input["input"]} > ${output["output"]}"
```
- Запуск скрипта с параметрами:
```bash
${resource["dcsaap-python"]} ${resource["my-script"]} -- --keys A B C --columns D E F --something-else
```
