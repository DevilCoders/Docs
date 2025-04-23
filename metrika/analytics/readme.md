## Metrica Analytics

### Arc и работа с репозиторием

1. Как работать с arc - https://docs.yandex-team.ru/devtools/intro/quick-start-guide
2. Кодстайл в аркадии - https://docs.yandex-team.ru/arcadia-python/python_style_guide

### Прекоммитные хуки
1. Прекоммитный хук - это скрипт, который выполняется перед каждым коммитом. Сейчас в нашем конфиге только форматтер. Добавить его можнно так, на той машинке, откуда планируете делать pr
    ```
    cat ~/arcadia/metrika/analytics/.arcconfig > ~/.arcconfig
    ```
### Форматтер и линтер
1. В тулзах уже есть дефолтный форматтер black. Если вызвать его просто так, то он отформатирует весь код, ничего не справшивая. А если добавить опцию `--diff`, то покажет как бы исправил файл
    ```
    ya tool black --line-length=200 -S --exclude='config|deprecated' --diff --color /path/to/my/file
    ```
2. Линтер покзывает ошибки по стилю. Можно использовать аркадийный конфиг, чтобы прогнать свой код с ним. В дефолтном конфиге там более строгие правила PEP8
    ```
    flake8 path/to/my/file --config=arcadia/build/config/tests/flake8/flake8.conf
    ```
### Разное

1. Группа metrica-analytics в аркадии - https://a.yandex-team.ru/arc_vcs/groups/metrika-analytics
