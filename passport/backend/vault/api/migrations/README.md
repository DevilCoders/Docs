# Миграция БД в Секретнице

Для миграции базы данных используем [Alembic](http://alembic.zzzcomputing.com/en/latest/) и расширение [Flask-Migrate](http://flask-migrate.readthedocs.io/en/latest/).

Команды для миграции вызываем через ```./vault_api db``` на дев-машинах. На проде и в тестинге команды для миграций нет.

## Разработка

* Запускаем ```./vault_api db upgrade```, чтобы обновить локальный vault_development.sqlite.
* Создаем новую миграцию ```./vault_api db migrate -m "new migration"```. Alembic проанализирует модели и построит новый файл с миграцией в папке [passport_vault/migrations/versions](versions).
* Редактируем файл с миграцией и проверяем, что миграция сработала, через ```./vault_api db upgrade```
* Добавляем ссылку на файл миграции в макрос DATA в passport/backend/vault/api/tests/ya.make

Если миграция не сгенерировалась, стираем файл vault_development.sqlite и повторяем шаги, начиная со второго.

Миграции автоматически накатываются на локальную базу, когда запускаем ```./vault_api run```

### Особенности

Внешним ключам обязательно указывать имя. Лучше всего все ограничения и индексы выносить в переменную \_\_table_args\_\_ модели:

```
__table_args__ = (
    ForeignKeyConstraint(['secret_uuid'], [Secret.uuid], name='secret_versions_ibfk_1'),
    Index('idx_secret_versions_secret_uuid', 'secret_uuid'),
    Index('idx_secret_versions_created_at', 'created_at'),
    Index('idx_secret_versions_created_by', 'created_by'),
)
```

Если миграция создает публичный ключ, то добавляем удаление внешнего ключа в метод downgrade:

```
with op.batch_alter_table('secret_versions') as batch_op:
    batch_op.drop_constraint('secret_versions_ibfk_1')
```

Используем batch_alter_table для удаления полей и ограничений, чтобы миграция не сломалась на SQLite:

```
with op.batch_alter_table('secret_versions') as batch_op:
    batch_op.drop_constraint('secret_versions_ibfk_1')
op.drop_table('secret_versions')
```

Про батчи в доке Алембика — http://alembic.zzzcomputing.com/en/latest/batch.html
