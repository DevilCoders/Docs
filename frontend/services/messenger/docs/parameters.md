# Параметры

### chatRestrictions

Правила фильтрации чатов. Параметр может использоваться для контроля чатов,
которые отображаются в списках, считаются при подсчете непрочитанных, и отображают
уведомления.

**Тип:** encode json-строки.

**Пример:** `?chatRestrictions=%7B"default"%3A"disabled"%2C"private"%3A"enabled"%2C"enabled"%3A%7B"groupsNS"%3A%5B4%5D%7D%7D`

Сниппет для получения корректной строки:
```javascript
encodeURIComponent(JSON.stringify({
    default: "disabled",
    private: "enabled",
    enabled: { groupsNS: [0] }
}));
```

Объект должен удовлетворять json-схеме: https://github.yandex-team.ru/serp/chat/blob/dev/src/configs/chatRestrictions.scheme.json

Внимание! На текущий момент в нем нельзя фильтровать роботные чаты, т.к. они не везде отличимы от приватных.

В случае не валидности переданного объекта по этой схеме, он не будет использован и применятся
стандартные правила отображения чатов.
