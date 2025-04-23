# Шаблон для создания новых сервисов

Чтобы его использовать, установи себе локально cookiecutter:

    pip3 install cookiecutter
    
Затем следуй нескольким простым шагам:

## Запусти кукикаттер и ответь на пару вопросов

Запускать надо с указанием `PYTHONPATH`:

```sh
PYTHONPATH=tools/cookiecutter:$PYTHONPATH cookiecutter tools/cookiecutter/service
```

У вопросов будут в квадратных скобках указаны дефолтные значения.
Если что-то не подходит, то нужно ввести новое значение:

```sh
maintainer [Alexander Artemenko <art@yandex-team.ru>]:
module_name [some_product_etl]: b2b_etl
dashed_name [b2b-etl]:<Enter>
Select gp_default_select_grant: # Доступ на select ко всем создаваемым объектам в Greenplum
1 - developer_mlu               # Для разработчиков Райдтеха и Фудтеха
2 - developer_market            # Для разработчиков Маркет
Choose from 1, 2 [1]: 1
```

В результате получится такая структура папок:

```
[art@macbook] tree b2b_etl
b2b_etl
├── b2b_etl
│   ├── __init__.py
│   └── layer
│       ├── __init__.py
│       └── example_dashboard
│           ├── __init__.py
│           └── loader.py
├── config_service
│   ├── default
│   │   └── logging.yaml
│   └── production
│       ├── accident.yaml
│       ├── logging.yaml
│       └── system.yaml
├── debian
│   ├── changelog
│   ├── compat
│   ├── control
│   ├── rules
│   ├── yandex-taxi-dmp-b2b-etl-cron.dirs
│   ├── yandex-taxi-dmp-b2b-etl-cron.environment
│   ├── yandex-taxi-dmp-b2b-etl-cron.install
│   ├── yandex-taxi-dmp-b2b-etl-cron.postinst
│   ├── yandex-taxi-dmp-b2b-etl.conf.tmpl
│   ├── yandex-taxi-dmp-b2b-etl.dirs
│   ├── yandex-taxi-dmp-b2b-etl.install
│   └── yandex-taxi-dmp-b2b-etl.prerm
├── service.yaml
├── setup.py
├── spark
│   └── b2b_etl
│       └── build.gradle.kts
├── test_b2b_etl
│   ├── __init__.py
│   ├── doc_test.py
│   └── workflow_test.py
└── workflow
    └── crontabs
        ├── workflow-cron-production
        ├── workflow-cron-testing
        └── workflow-task-cron-testing

12 directories, 29 files
```

## Скопируй настройки для спарка в отдельную директорию

```
[art@macbook] mv b2b_etl/spark/b2b_etl ./spark
[art@macbook] rm -fr b2b_etl/spark
```

