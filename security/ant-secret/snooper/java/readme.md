JNI биндинг
===
**TBD**

jar'ник в Artifactory: http://artifactory.yandex.net/artifactory/yandex_security_releases/ru/yandex/security/snooper-java/

Пример использования:
```C++
// Инстанцируем Snooper
// Внимание! Snooper НЕ thread-safe в угоду производительности
NativeSnooper snooper = new NativeSnooper();

// Теперь мы можем поискать секретики БЕЗ валидации:
Secret[] secrets = snooper.search(line);

// Или С валидацией:
Secret[] secrets = snooper.searchValidated(line);

// А можем просто замаскировать все встретившиеся секретики БЕЗ валидации:
String out = snooper.mask(line);

// И С валидацией:
String out = snooper.maskValidated(line);
```

Пожалуйста, не пользуйтесь валидацией без нужды (для простого маскирования она не нужна).