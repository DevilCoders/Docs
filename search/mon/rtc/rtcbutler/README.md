Для корректной работы exporter, нужно добавить индексы на базу:
```
db.to_export.lock.ensureIndex( { aid: 1 }, {unique: false} );
db.to_export.lock.ensureIndex({date: 1}, {expireAfterSeconds: 30});
```
