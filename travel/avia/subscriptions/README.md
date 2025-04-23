# subscriptions
Сервис подписок на всякие обновления

Необходимые для запуска настройки можно найти в app/api/settings.
Настройки могут быть переданы через:
1. Конфигурацию `settings/config.py`
2. Переменные окружения

Наибольший приоритет у переменных окружения.

Для опеределения конфигурации используется переменная окружения `YANDEX_ENVIRONMENT_TYPE`.
Для настройки логгирования используется переменная окружения `AVIA_LOG_PATH`.
Для определения токена от секретницы используется переменная окружения `YAV_TOKEN`.
Остальные настройки можно закидывать в конфигурационный файл.

Для получения секретов рекомендуется использовать секретницу yav.yandex-team.ru.
Секреты автоматически будут подставлены вместо их идентификаторов (sec-abcde.., ver-abcdef...).
Если в секрете больше одного поля, то необходимо через точку указать какое именно поле необходимо подставить (Пример: `sec-abcdef123.password`)

При необходимости добавить что-то в конфигурацию приложения - расширяем app/api/settings.
Новые настройки будут подхвачены автоматически из перечисленных выше источников.
Если у какой-то настройки нет значения по умолчанию, она считается обязательной и приложение не запутится, пока данная настройка не будет поставлена через источники.


## Cтандартный запуск
### Приложение

```(bash)
cd $ARCADIA_ROOT/travel/avia/subscriptions
ya make
cp tools/samples/environments.sh tools/
vi tools/environments.sh
./tools/environments.sh
./app/bin/app
```

### Тесты

```(bash)
ya make -tt
```

При тестировании поднимается локальный _postgres_, все настройки для подключения
 кладутся в переменные окружения `PG_LOCAL_*`.

 При запуске тестов после каждого теста запускается автоматическая фикстура
 `truncate_db` для отчистки всех таблиц за исключением, когда есть маркер `pytest.mark.no_truncate`
 или не используется ни одна модель базы данных (_pytest_ автоматически разворачивает
 список используемых фикстур, включая фикстуры, используемые внутри переданных, поэтому
 модели БД могут присутствовать __неявно__)

## Docker

### Сборка

Перед тем, как начать сборку, необходимо быть заголиненным в registry.yandex.net:
```(bash)
cat your_ya_token | docker login -u ${yandex_login} --password-stdin registry.yandex.net
```

```(bash)
ya package api-pkg.json --docker --docker-repository=avia
```

### Запуск

Стандартный конфиг для запуска Docker находится в `tools/samples/dev.env`

```
docker run --rm -ti --env-file=tools/dev.env registry.yandex.net/avia/subscriptions:{branch}.{revision}.{sandbox_task_id}
```

- `revision` - текущая ревизия, берется от корня исходников
- `branch` - текущая ветка
- `sandbox_task_id` - ИД Сандбокс-таски, при сборке пакета через задачу YA_PACKAGE

### Публикация

```
docker push registry.yandex.net/avia/subscriptions:{branch}.{revision}.{sandbox_task_id}
```

### Миграции

Все скрипты миграции находятся в бинарнике `subscriptions/app/alembic/bin/alembic_tool`, поэтому для работы с ними,
перед запуском алембика они дампятся в файловую систему. По дефолту, извелечение происходит в текущую директорию,
но ее можно изменить с помощью переменной окружения `TRAVEL_SUBSCRIPTIONS_MIGRATIONS_EXTRACT_DIR`

```(bash)
cd $ARCADIA_ROOT/travel/avia/subscriptions
ya make
cd app/
./alembic/bin/alembic_tool [args]
```

Если хотим изменить директорию извлечения ресурсов, то
```(bash)
TRAVEL_SUBSCRIPTIONS_MIGRATIONS_EXTRACT_DIR=some_dir ./alembic/bin/alembic_tool [args]
```

Также можно добавить путь до бинарника в `PATH`

Для того, чтобы накатить миграции необходимо:
```(bash)
cd $ARCADIA_ROOT/travel/avia/subscriptions/app
./alembic/bin/alembic_tool upgrade head
```

#### Важно
После создания файла с миграцией его __необходимо__ добавить в `ya.make` (в секцию `RESOURCE_FILES`),
иначе при выкатке приложение не увидит вашу миграцию.
