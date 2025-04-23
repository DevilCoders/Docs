# drills-helper

Cli-тулза для управления учениями в Вертикалях. Сейчас умеет: 
* Выключать деплой в shiva, conductor, jenkins;
* Проставлять аннотации на все действия. 

Wiki: https://wiki.yandex-team.ru/vertis-admin/drills-helper

## Разработка 

Для запуска приложений и тестов требуется grafana:
```
docker-compose up -d
```

Для тестов используются в основном тестовые сервисы(shiva, jenkins, conductor).

### Конфигурация

Для локального запуска и прогона тестов нужны секреты в файле `local.env` в корне проекта.

Получение этих секретов описано в [вики](https://wiki.yandex-team.ru/vertis-admin/drills-helper#sekrety)

Для локального запуска и тестов используется `local.env` и сооветвуствующий проекту `dev.env`

#### schema-registry

Для генерации связанных api proto-файлов используем [schema-registry](https://github.com/YandexClassifieds/schema-registry)
- Для первого использования: `git submodule init`
- внести изменения в [schema registry](https://github.com/YandexClassifieds/schema-registry)
- `git submodule update --remote`
- `make protos`

### Локальный запуск

Собрать бинарь и запустить.    

### Тесты

Требуются Docker-контейнеры: `docker-compose up -d`

Запуск через `make test`. 

### Перед пушом
```shell
make format
make lint
make test
```