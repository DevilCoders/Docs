# appUsageWakeUpInterval
**Type:** Long
**Default:** 10,800,000 (3 часа)

**Related tickets**
[TVANDROID-4438](https://st.yandex-team.ru/TVANDROID-4438)

**Context**
```json
{
  "com.yandex.tv.services": {
    "appUsageWakeUpInterval": "value"
  }
}
```

**Description**
Интервал в который запрашиваем из системы статистику по использованию апп. Если <= 0, будет использоваться старый механизм (неточный). 
