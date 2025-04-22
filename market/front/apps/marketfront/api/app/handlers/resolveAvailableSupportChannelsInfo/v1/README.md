# Получение информации о доступных способах связи со службой поддержки из CMS  (resolveAvailableSupportChannelsInfo)

**Request:**
```js
{
  "params": [
    {} // никакие параметры прокидывать не нужно
  ]
}
```

**Логика работы хэндлера:**
1. Используя темплатор, идёт в CMS на страницу https://cms.market.yandex.ru/editor/documents/123665/edit (тип материала - "Покупки / доступные способы связи со службой поддержки")
2. Получает данные из CMS, нормализует и отдаёт их в формате, представленном ниже в примере ответа

**Пример ответа:**
```js
{
    "results": [
        {
            "handler": "resolveAvailableSupportChannelsInfo",
            "result": "current"
        }
    ],
    "collections": {
      "availableSupportChannelsInfo": {
        "current": { // id коллекции всегда одинаковое - "current"
          "id": "current"
          "isChatAvailable": true,
          "isPhoneAvailable": true,
          // текст или html, который нужно вставить вместо телефона поддержки, если он недоступен
          "unavailablePhoneText": "",
        },
      },
    }
}
```
