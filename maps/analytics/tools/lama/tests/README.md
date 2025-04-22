# Тестируем на pytest

Так как сеть нестабильна, нужно глушить все запросы.
Для этого доступна глобальная фикстура `mock_api`, которая будет заглушкой для всех `http` запросов.

Все запросы будут лежать в файле `responses.json`. Файл можно модифицировать только автоматикой.

***

## Пример функции самого теста

```
def test_sync():
    full_path = get_path('lama.yaml')
    SyncCommand().exec(full_path, {'reactor': False})

```

***

## Обновление фикстур (пока для пресетов для юнит тестов)

Чтобы вручную не настраивать каждую фикстуру, добавленную в тесты есть скрипт `update-fixtures`. Нужно только добавить `yaml` файл, остальное сделает автоматика.
При изменении пресетов нужно просто запустить скрипт

1) Читаем папку в `unit` тестах с фикстурами
2) Находим все файлы, которые заканчиваются на `.in.yaml`
3) Генерируем ожидаемый файл `${filename}.out.json`
4) Модифицируем `ya.make` для тестов, обновив список ресурсов

***

## Полезные ссылки
- https://auth0.com/blog/mocking-api-calls-in-python/#Mocking-Third-Party-Functions
- https://requests-mock.readthedocs.io/en/latest/index.html
- https://realpython.com/testing-third-party-apis-with-mocks/
- https://pypi.org/project/pytest-mock/

- https://clubs.at.yandex-team.ru/arcadia/21691

