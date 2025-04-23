## Скрипт `write_env_to_file.py` перезаписывает файл с переменными окружения
### Входные параметры:
1. ``--input_file`` - входной файл с первоначальными переменными окружения.
#### Примерная архитектура файла:
```angular2html
export ENV_VAR_NAME1 = EMV_VAR_VALUE1
export ENV_VAR_NAME2 = EMV_VAR_VALUE2
export ENV_VAR_NAME3 = EMV_VAR_VALUE3
```
2. ``--output_file`` - файл для записи полученного множества переменных окружения
3. ``--json`` - `*.json` файл, который создается strongbox-ом внутри содержит словарь с секретами.
4. ``--additional_sections`` - список дополнительных секций словаря (помимо `ENV`), из которых брать секреты, через пробел.
### Команда использования скрипта:
``python write_env_to_file.py --input_file <входной файл> --output_file <выходной файл> --json <файл с секретами от strongbox> [--additional_sections <секция 1> ... <секция N>]``


## Скрипт download_tanker_translate.py загружает из танкера переводы для задаваемых проектов:
### Входные параметры:
1. `oauth` - OAuth токен
2. `type_api` - Тип api, потому как на момент написания поддерживался [старый](https://doc.yandex-team.ru/Tanker/api-reference/concepts/about.xml) и [новый](https://wiki.yandex-team.ru/l10n/tanker/). Соответственно данный параметр имеет только 2 значения `new` и `old`
3. `env` - тип запроса `production` или `test`, если не задавать, то по-умолчанию `test`
4. `project` - название проекта в Танкере
5. `path_to_save` - путь для сохранения итоговых результатов.

### Команда использования скрипта:
``python download_translate_from_tanker.py --oauth <токен> --type_api <new или old> --env <test или production> --project <название проекта> --path_to_save /path/to/save``
