# Выборка бизнес-объектов

Для получения бизнес объектов существуют следующие методы:

  Примеры использования данного API:
  - Получение объекта по GID
    ```groovy
    api.db.get('test@123')
    // or
    api.db.of('test').get('test@123')
    // but you could not fetch instance of another class
    api.db.of('test').get('another@123') // throws IllegalArgumentException
    ```
  - Получение объекта по значению naturalId атрибута
    ```groovy
    api.db.of('brand').get('beru')
    ```
  - Получение объекта по идентификатору `id`
    ```groovy
    api.db.of('test').get(1234)
    ```
  - Выборка объектов
    - Простая выборка всех объектов
      ```groovy
      api.db.of('test').list()
      ```
    - Подсчет всех объектов
      ```groovy
      api.db.of('test').count()
      ```
    - Можно использовать `offset` и `limit`
      ```groovy
      api.db.of('test')
        .offset(5)
        .limit(4)
        .list()
      
      // but count with offset/limit will throw an error
      // because it's undefined operation in SQL
      api.db.of('test')
        .offset(5)
        .limit(4)
        .count() // NoSuchMethod
      ```
    - Сортировка результата
      ```groovy
      api.db.of('test')
        .withOrders(
          api.db.orders.asc('attribute1'),
          api.db.orders.desc('attribute2')
        )
        .limit(10) // offset/limit could be applied
        .list()
      
      // but count with withOrders will throw an error
      // because it's meaningless to count with sorting
      ```
    - Фильтрация результата
      ```groovy
      api.db.of('test')
        .withFilters(
          api.db.filters.eq('attribute1', 123),
          api.db.filters.or(
            api.db.filters.in('attribute2', [1,2,3]),
            api.db.filters.containsAll('attribute3', [5,6,7])
          )
        )
        .count()
      ```
      
      Либо есть способ описать фильтры отдельно, но более лаконично
      ```groovy
      def filters = api.db.filters.with {[
        eq('attribute1', 123),
        or(
          delegate.in('attribute2', [1,2,3]), // take attention to delegate. Use it, because 'in' is keyword 
          containsAll('attribute3', [5,6,7])
        )
      ]}
      api.db.of('test')
        .withFilters(filters)
        .count()
      ```
      
      Но этот способ так же не единственный альтернативный.
      Можно описывать фильтры прямо на месте, только используя специальный синтаксис
      ```groovy
      api.db.of('test')
        .withFilters {
          eq('attribute1', 123)
          or {
            // take attention to _in. Underscore here used, because 'in' is a keyword. It automagically resolved
            _in('attribute2', [1,2,3]) 
            containsAll('attribute3', [5,6,7])
          }
        }
        .count()
      ```
      
      Специальность синтаксиса проявляется в том, что `withFilters`, а так же все junction фильтры (e.g. `and`, `or`)
      нужно использовать с блоком кода `{}` (`Closure`). Все остальные фильтры используются как обычно
    - Получение результата в единственном числе
      ```groovy
      api.db.of('test').get()
      api.db.of('test').withFilters({ eq('attribute1', 123) }).get()
      api.db.of('test').limit(1).get()
      ```
      Все эти варианты вернут `null`, если нет результата, сам объект, если он один,
      и выбросят `javax.persistence.NonUniqueResultException`, если результат не уникален
  - Выборка объектов с помощью HQL
    ```groovy
    api.db.query('''
      FROM ticket t
      WHERE t.responsibleEmployee.gid = :responsibleGid
        AND t.creationTime > :threshold
    ''')
      .responsibleGid(api.security.responsible.gid)
      .threshold(OffsetDateTime.now().minusDays(5))
      .list()
    ```
    Обратите внимаение на то, как указываются переменные из тела запроса:
    просто вызываем соответствующий метод с указанием значения
    
    Так же можно ограничить размер результата
    ```groovy
    api.db.query('FROM ticket')
      .limit(10)
      .list()
    ``` 
    
    И получить один объект
    ```groovy
    api.db.query('FROM ticket')
      .limit(1)
      .get()
    ```
  - Проверка существования объектов по критерию
    ```groovy
    assert !api.db.of('test').any() // equal to api.db.of('test').limit(1).get() != null
    // with filters
    boolean exists = api.db.of('test')
      .withFilters { eq('attr', 'value') }
      .any()
    // or HQL
    api.db.query('FROM test').any()
    ```

  -  Загрузка LAZY-атрибутов объектов (полезно для уменьшения кол-ва запросов к БД)

    ```groovy
    api.db.of('test')
      .withFilters({ eq('attribute1', 123) })
      .withAttributes('lazyAttr1Code', 'lazyAttr2Code')
      .list()
    ```

    Список необходимых атрибутов можно дополнять по необходимости при помощи метода addAttributes 
    ```groovy
    api.db.of('test')
      .withAttributes('lazyAttr1Code', 'lazyAttr2Code')
      .withFilters({ eq('attribute1', 123) })
      .addAttributes('lazyAttr3Code', 'lazyAttr4Code')
      .list()
    ```
