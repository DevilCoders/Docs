# Ресурс /feeds/templates

## GET /feeds/templates

Получение excel-шаблона, соответствующего переданной категории. Возвращает сам шаблон (Content-type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet).
Доступ к ручке имеет авторизованный пользователь.

### Примечания
  - Пример вызова 
  
  `curl vendor-partner.tst.vs.market.yandex.net:34868/feeds/templates?uid=1999&categoryId=91491 > template.xlsx`
  

### Параметры
  - **uid** `<UID>` - сейчас необязательный параметр из-за [бага](https://st.yandex-team.ru/VNDMARKET-53)
  - **categoryId** `<int>` - идентификатор категории, для которой будет возвращен шаблон

### Ответ

  Excel-файл, содержащий шаблон, соответствующий переданной категории

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
 - 404 (NOT_FOUND) если не найден шаблон, соответствующий переданной категории
 - 500 (INTERNAL_ERROR) если IR вернул статус INTERNAL_ERROR

