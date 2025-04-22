**Как запустить вывод ответственных для списка стейджей**

Обычный запуск sidecars updater выглядит так: `java -jar sidecars_updater.jar <path_to_config>`.
Чтобы запустить режим вывода ответственных, надо просто добавить вторым аргументом путь до файла со стейджами.
Порядок действий:
1. `cd <arcadia_path>/infra/deploy_sidecars_updater`
2. `ya make`
3. `java -jar sidecars_updater.jar <path_to_config> <path_to_stages>`

Конфиг может выглядеть так:
```
yp = {
    master = {
        host = "xdc.yp.yandex-team.ru"
    }
    token = <yp_token>
}
sandbox = {
    token = ""
}
staff = {
    token = <yp_token>
}
startrek = {
    token = ""
}

```

Id стейджей в файле должны быть на новой строке:
```
stage1
stage2
stage3
```
