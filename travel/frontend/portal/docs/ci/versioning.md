## Versioning

### Docker

Для версионирования докер образов используется версионирование из CI

```
${context.version_info.full}
```

, где `${context.version_info.full}` - это номер релиза.

```
1, 2, 3 - новый релиз
1.1, 1.2, 1.3 - исправления внутри релизов
```

`${context.target_commit.revision.number}` - номер ревизии Arc.

### NPM

Для пакетов npm используется следующая схема

Мажорная версия берется из `package.json`.
Минор и патч берется из CI.

То есть если потребуется

1. выпустить минорную версию - запустить релиз от trunk
2. выпустить патч - запустить релиз от релизной ветки соответствующего минора
3. выпустить мажор - обновить мажорную версию в `package.json` и создать новый тип релиза в CI,
   чтобы обнулить счетчик версии. Выпускать предыдущий мажор можно будет через старый релиз.
