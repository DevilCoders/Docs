# 1.0.0

**PR:** [#2499340](https://a.yandex-team.ru/review/2499340)
**Author:** @gheljenor **Date:** 2022-04-26

[undefined](https://st.yandex-team.ru/undefined) - undefined

### Usage

```javascript
const configs = require('@yandex-market/configs');

// Все параметры опциональные, здесь указаны их дефолтные значения.
module.exports = configs({
    root = Path.resolve(process.cwd(), 'configs'), // - путь к директории с конфигами
    environment = process.env.YENV || 'current', // - название текущего окружения
    envPrefix = 'appConfig', // - префикс переменных окружения для переопределения конфигов
    nestedRoot = true, // - см. особенности
    nestedEnv = true, // - см. особенности
})
```

### Migration

Переезд в монорепу. Первая версия.