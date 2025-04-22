## Установка:
```
$ conda install seaborn pillow
$ pip install ta-report -i https://pypi.yandex-team.ru/simple/
```

## Использование:
```(sh)
$ cd {work_dir}
$ ta-report -h
```

## Dev
### Добавление/удаление вкладки

Сборщик для каждого отчета определен в init-файле модуля. Например, для отчета "Настройки ТГО": `ta_report/xlsx_keywords/__init__.py`

Не забыть и поправить файлы:
- `test/test_cli.py` — для проверки наличия
- `ta_report/sheets.yml` — для перевода и пресетов
