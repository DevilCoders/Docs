# Обертка над формой создания/редактирования условия

Что делает:
Если conditionId не передан - создает пустую форму создания условия
Если conditionId передан - получает данные условия по id (web-api) и создает форму в режиме редактирования
При вызове метода save - сохраняет условие в web-api

Пример использования

```
    block: 'b-retargeting-condition-wizard'
    conditionId: 666,
    isReadOnly: false
```

События:
ready - форма готова
change - форма изменилась
