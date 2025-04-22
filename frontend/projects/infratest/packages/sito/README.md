# sito

Модуль для проверки строки на соответствие набору правил, язык которых повторяет 
язык правил, используемый в переменной окружения `DEBUG` одноименным модулем.

## Пример использования

```typescript
import sito from "@yandex-int/sito";
const filter = sito(process.env.DEBUG);
const isMyModuleEnabled = filter("mymodule");
```

