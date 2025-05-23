# Рассылятор B2B

Что где:
* вики-страница проекта [/fan](https://wiki.yandex-team.ru/fan/)
* немного документации [docs](docs)

## Разработчику

### Поднять проект локально

Поднять Django сервер вместе со вспомогательными сервисами - кроме контейнера с тасками:
```bash
make devup
```

> Локальная база хранит данные в .pg_data директории в корне проекта, поэтому если нужно пересоздать базу с нуля, то нужно удалить каталог .pg_data.

#### Миграции и тестовый юзер

`make devfaststart` накатит на локальную базу миграции, создаст суперпользователя `root`с паролем `root`, создаст аккаунт `dev` и выдаст пользователю `root` роль модератора в аккаунте `dev`. Все тоже самое можно сделать следующими командами по порядку:

> `make devmanage cmd="{command}"` запустит manage.py команду {command} внутри dev-контейнера

1. накатить миграции:
    `make migrate`

2. создать суперпользователя:

    `make devmanage cmd=createsuperuser`

3. создасть аккаунт `dev`:

    `make devmanage cmd="create-account --id=dev --title=Dev --domain=yandex-team.ru"`

4. выдать пользователю роль модератора в аккаунте:

    `make devmanage cmd="grant-account-access --account-id=dev --role-name=moderator --username=<username>"`

Далее заходим в админку `https://localhost:8000/admin/` и логинимся.

После логина переходим на главную `https://localhost:8000/`.

### Прогнать тесты
- `make test` - собрать тестовые контейнеры и прогнать тесты всех компонентов
- `make test-ui` - собрать тестовый образ и запустить тесты для UI компонента
- `make test-feedback` - собрать тестовый образ и запустить тесты для Feedback компонента
Можно передавать дополнительные аргументы: `make test-ui extra="-k test_bounce.py"`

### Докер
- `make docker-clean` - почистить ранее собранные образы
- `make docker-build` - собрать все образы для релиза с тегом :local
- `make docker-tag version="<version>"` - потегать образы конкретной версией
- `make docker-push` - залить образы в registry.yandex.net/mail/fan/
У целей есть версии для одного компонента. Например, чтобы собрать UI, надо запустить `make docker-build-ui`. Это используется в сборочных джобах для сборки конкретных компонентов.
- `make docker-build-pybase` - собрать базовый образ и установить ему таг
- `make docker-push-pybase` - залить собранный базовый образ в репозиторий

### Другие команды
- `make migrate` - накатить миграции на локальную базу
- `make makemigrations` - сгенерировать миграции
- `make tcmd cmd={cmd}` - запустить команду `{cmd}` в тестовом контейнере UI<br>
    Например, запустить bash: `make tcmd cmd=bash`, и внутри набрать `pytest {some_test}` чтобы по-быстрому запускать модуль с тестами `{some_test}` без пересозданий контейнера, как в случае с командой `make test`
- `make clean` - почистить все временные файлы: кэш, логи и .pg_data

###### Формат кода
- `make sort-imports` - автосортировка импортов в модулях
- `make check-style` - проверка flake8 и сортировки импортов
- `make cc` - отсортирует импорты и запустит проверку flake8 - **сейчас flake8 фейлится - нажно поправить огрехи в коде прежде чем заносить шаг проверки формата в сборку**
- `make autopep8` - автоформатирование кода в лайтовом режиме (без aggressive) - поправит мелкие огрехи с переносами и пробелами

- `make pyclean` - удалить артефакты python (кеш, байткод)
- `make devstop` - остановить все dev сервисы
- `make devdown` - удалить контейнеры dev-сервисов (так как лоальная база хранит данные в .pg_data через байнд маунт, то сама база не пропадет)
