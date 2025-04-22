# adv_backend 🔙

Бэкенд [Сайта Рекламы](https://yandex.ru/adv)

[Тестовое окружение](https://deploy.yandex-team.ru/project/advertising-backend-test) в Yandex Deploy

## Основные комманды

### Инициализировать локальное окружение

```
make init
```

Перед запуском убедиться, что у вас установлен локальный PostgreSQL

### Подтянуть данные из Бункера

```
make b2d
```

### Собрать бинарник

```
make build
```

### Создать миграцию

```sh
make makemigrations app=backend name=my_migration
```

В `app` указываем приложение, для которого нужно создать миграцию  
В `name` опционально можно указать собственное имя для миграции

### Запустить сервер

```
make run
```

### Накатить миграции

```
make migrate
```

### Собрать и запушить Docker-образ

```
make publish tag=0.1
```

### Запустить тесты

```
make test
```

Во время тестов локальная база не нужна, она будет собрана из [рецепта](https://a.yandex-team.ru/arc/trunk/arcadia/commerce/adv_backend/recipes/postgresql/recipe.inc)
