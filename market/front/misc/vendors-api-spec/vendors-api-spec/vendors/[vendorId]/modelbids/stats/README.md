# Ресурсы группы /vendors/[vendorID]/modelbids/stats/

## GET /vendors/[vendorID]/modelbids/stats/[stat]

### Возможные значения `[stat]`:
1. `model-clicks` - Отчёт по кликам на модель (id выборки: `modelbids:model-clicks`)
2. `category-clicks` - Отчёт по кликам на категорию (id выборки: `modelbids:category-clicks`)
3. `category-model-position` - Отчёт по среднему значению позиции в каталоге (id выборки: `modelbids:category-model-position`)
4. `category-model-charges` - Отчёт по расходам (детальный) (id выборки: `modelbids:category-model-charges`)
5. `shows` - Отчёт по показам карточки в выдаче (id выборки: `modelbids:shows`)

### Параметры
  - **uid** `<UID>`
  - modelId `<Number>` (поддерживается для `model-clicks`, `category-model-position`, `category-model-charges`, `shows`) -
   идентификатор модели вендора, для которой нужно получить статистику.
  - categoryId `<Number>` (поддерживается для `category-clicks`, `category-model-position`, `category-model-charges`, `shows`) -
   идентификатор категории вендора, для которой нужно получить статистику.
  - from `<DateTime>` - дата (в UTC), идентифицирующая месяц, за который нужно получить статистику
     (любой момент времени между `00:00` первого числа месяца, и `23:59:59.999` последнего числа месяца, включительно).
     По умолчанию - текущие дата и время.

### Ответ
<[SimpleResponse](/_entities/responses/SimpleResponse.md) [[StatResult](/_entities/stats/StatResult.md)]>

### Примечания
  - Для всех статистик, работающих, и с `categoryId`, и с `modelId` - можно передавать **либо** `categoryId`, **либо** `modelId`, либо ни один из них.

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Некорректная дата](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

## GET /vendors/[vendorID]/modelbids/stats/[stat]/download

Всё то же самое, что и у родительской ручки, кроме типа ответа.
В ответ приходит публично-доступная ссылка на CSV-файл с данными статистики.

### Дополнительные параметры
  - format `CSV|XLSX` - формат файла (по умолчанию CSV)

### Ответ
<[SimpleResponse](/_entities/responses/SimpleResponse.md) [[HtmlLink](/_entities/HtmlLink.md)]>