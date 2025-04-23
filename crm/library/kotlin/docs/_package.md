### Package layout

Абстракции кладём в корень папки.
Реализации, завязанные на фреймворк, кладём в подпапку с названием фреймворка.
Реализации, не завязанные на фреймворк, кладём в папку `impl`.

{% cut "Example" %}
```
.../entity/
  repository/
    EntityMetaRepository
    EntityRecordRepository
    jooq/
      JooqEntityMetaRepository
      JooqEntityRecordRepository
    hibernate/
      HibernateEntityMetaRepository
      HibernateEntityRecordRepository
  manager/
    EntityManager
    impl/
      EntityManagerImpl
```
{% endcut %}
