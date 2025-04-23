# Контентная админка

Подробное описание проекта https://wiki.yandex-team.ru/travel/kontentnyjj-razdel/

### Сборка статики локально

Создаем bin/app/local_settings.py:
```python
from travel.marketing.content.admin.settings import *  # noqa

DEBUG = True
STATIC_ROOT = "static"
```

Собираем бинарник:
```
ya make -D RASP_DEV .
```

Затем запускаем сборку статки:
```
DJANGO_SETTINGS_MODULE=local_settings Y_PYTHON_ENTRY_POINT=travel.marketing.content.admin.app:manage ./app collectstatic
```

В bin/app должна появиться папка static. Добавляем в local_settings
```
PROJECT_PATH = os.path.abspath(os.path.join(os.path.dirname(__file__)))
STATICFILES_DIRS = [os.path.join(PROJECT_PATH, "static")]
```

После этого статика должна коректно работать если запускать через gunicorn.
Для запуска через manage нужно закоментировать STATIC_ROOT

### запуск через gunicorn
```
RASP_VAULT_OAUTH_TOKEN=$VAULT_TOKEN DJANGO_SETTINGS_MODULE=local_settings Y_PYTHON_ENTRY_POINT=travel.marketing.content.admin.app:gunicorn ./app
```

#### notes:
- При локальном запуске может не работать аутентификация, можно разбираться как починить,
а можно написать middleware, которая обновляет request.user:
    ```python
    class UpdateUser(object):
        def __init__(self, get_response):
            self.get_response = get_response

        def __call__(self, request):
            request.user = User.objects.get(username="$USERNAME")
            return self.get_response(request)
    ```
    и сделать её последней в цепочке `MIDDLEWARES`
- Чтобы локально запускаться с настройками из тестинга можно поменять проверку в `settings.py`:
  ```python
    if yenv.type == 'testing' or yenv.type == 'development'
  ```

### Миграции

Специфика миграций в PostgreSQL https://docs.djangoproject.com/en/3.1/topics/migrations/#postgresql

Запуск миграций пока производится только вручную:

```shell
RASP_VAULT_OAUTH_TOKEN=$VAULT_TOKEN DJANGO_SETTINGS_MODULE=local_settings Y_PYTHON_ENTRY_POINT=travel.marketing.content.admin.app:manage ./app makemigrations
vim ya.make # Добавляем миграцию в ya.make
ya make -D RASP_DEV . # Нужно пересобрать бинарник, чтобы в него добавилась миграция
RASP_VAULT_OAUTH_TOKEN=$VAULT_TOKEN DJANGO_SETTINGS_MODULE=local_settings Y_PYTHON_ENTRY_POINT=travel.marketing.content.admin.app:manage ./app migrate
```
