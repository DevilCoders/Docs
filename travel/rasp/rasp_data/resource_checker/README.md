# Что это?

Приложение, проверяющее целостность и правильность сгенерированных дампером ресурсов

Использует апи для чтения сгенерированных ресурсов из https://a.yandex-team.ru/arc/trunk/arcadia/travel/library/python/dicts

# Локальный запуск:
- Скачать необходимые ресурсы в `/app/data`
- В корне с этим README: `ya make && ./bin/app/app`

# Написать новую проверку:
- Создать новый или выбрать один из готовых файлов с проверками в `./checks`
- Написать проверку с сигнатурой `CHECK_TYPE` из [./checker.py](./checker.py). Проверка либо возвращает `None` при удачном результате, либо кидает [CheckException](./check_exception.py) с тескстом ошибки.
- Добавить новую проверку в список `CHECKS` из [./checks/\_\_init\_\_.py](./checks/__init__.py)
- Написать тесты на проверку (запуск через `ya make -tt`)

# Добавить ресурс, который ещё не проверяется:
- в `DataProvider` из [./data_provider.py](./data_provider.py) добавить соответствующий репозиторий.
- в `REPOS` из [./bin/app/main.py](./bin/app/main.py) добавить имя соответствующего файла ресурса.
- в `create_data_provider` из [./tests/utils.py](./tests/utils.py) добавить поддержку нового ресурса.

# Собрать sandbox-таск:
После того, как код будет смерджен в trunk, нужно запустить [scheduler](https://sandbox.yandex-team.ru/scheduler/696115/view) для сборки бинарной задачи.

Если перед мерджем хочется проверить работу таска, то можно через тот же scheduler собрать бинарь с патчем из PR (в поле `arcadia_patch` прописать `arc:pr_id`) и запустить `RASP_CHECK_RASP_DATA_RESOURCES` с получившимся бинарём.
