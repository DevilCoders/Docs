## Кубики используемые сервисом Композитор
https://abc.yandex-team.ru/services/compositor/

### Использование
Если не передавать `Y_PYTHON_ENTRY_POINT` - по умолчанию будет вызвана функция,
которая вернет ошибку (сделано, чтобы не забывали передавать).

Соответственно чтобы запустить нужную команду вызов такой:

```Y_PYTHON_ENTRY_POINT="intranet.compositor_processors.src.commands:create_org" 
./compositor.brick --input_file_path ${input["data"]} 
--output_file_path ${output["result"]}
```

`${input["data"]} и ${output["result"]}` зависят от того как кубик настроите, это названия заданные
на вкладке I/O кубика.

### Вызов click команды из кода

Стоит учесть, что такой вызов не запустит Click pipeline (валидацию аргументов и т.д.).
`click_command.callback(arg1, arg2)`

### Загрузка новой версии в нирвану

Пока руками - запустить `ya make --target-platform=linux .` и залить получившийся бинарник в нужный кубик.
Внимание - если собрать с `--target-platform=linux` на маке бинарник не запустится, если хотите локально
запускать - собирайте без этой команды.

### Посмотреть где лежит бинарник
```
ls -l ./src/program/compositor.brick 
lrwxr-xr-x  1 smosker  LD\Domain Users  81 20 ноя 12:52 ./src/program/compositor.brick -> /Users/smosker/.ya/build/symres/b40a7bf4ca23c994050fd2cc6e9733a7/compositor.brick
```

### Пример написания команды для кубика

Смотри файл `processors/example.py`

В целом нужно написать функцию такого вида:
```
@nirvana_command
def do_smth(org_name: str, org_id: int = None) -> dict:
```

Аннотация аргументов обязательна, функция должна возвращать либо ничего, либо 
словарь, который можно будет сдампить json'oм в файл (эти данные будут переданы в
следующий кубик)

Декоратор nirvana_command не влияет на исходную функцию, то есть ее можно импортировать и
использовать в любом месте кода при необходимости.

Декоратор помещает ее обернутый вариант в namespace модуля commands после чего она 
становится доступна для запуска через 
`Y_PYTHON_ENTRY_POINT="intranet.compositor_processors.src.commands:create_org"`

### Где посмотреть логи кубика

https://jing.yandex-team.ru/files/smosker/2019-11-19_11-41-38.png

### Где указать команду для запуска и переменные окружения

https://jing.yandex-team.ru/files/smosker/2019-11-19_12-17-17.png

### Использование TVM2

Если нужно из кода кубика сходить по TVM2 - нужно в настройках кубика указать:
1. Добавить в опции кубика опцию с типом `Secret`, назвать `tvm2_secret`, указать название секрета
2. Добавить переменную окружения кубика `YENV_TYPE=testing/production` (`testing` по умолчанию)
3. Добавить параметр запуска `--tvm2_secret ${param["tvm2_secret"]}`
4. В коде кубика вызывать `service_ticket = get_service_ticket(<service>_TVM_CLIENT)`
