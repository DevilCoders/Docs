# Ресурсы группы /vendors/[vendorID]/recommended/stats/

## GET /vendors/[vendorID]/recommended/stats/[stat]

### Возможные значения `[stat]`:
1. `clicks` - Отчет по кликам (CPC на предложения рекомендуемых магазинов, id выборки: `recommended:clicks`)
2. ~~`sales`~~ (пока недоступно) - Отчёт по продажам (CPA рекомендуемых магазинов, id выборки: `recommended:sales`)
3. `model-clicks` - Отчёт по кликам только в карточках где был хотя бы один рекоммендованный клик за месяц (id выборки: `recommended:model-clicks`)
4. `category-model-charges` - Отчёт по расходам (детальный) (id выборки: `recommended:category-model-charges`)

### Параметры
  - **uid** `<UID>`
  - modelId `<Number>` (поддерживается для `category-model-charges`) - идентификатор модели вендора, для которой нужно получить статистику.
  - categoryId `<Number>` (поддерживается для `category-model-charges`) - идентификатор категории вендора, для которой нужно получить статистику.
  - from `<DateTime>` - дата (в UTC), идентифицирующая месяц, за который нужно получить статистику
     (любой момент времени между `00:00` первого числа месяца, и `23:59:59.999` последнего числа месяца, включительно).
     По умолчанию - текущие дата и время.

### Ответ
<[SimpleResponse](/_entities/responses/SimpleResponse.md) [[StatResult](/_entities/stats/StatResult.md)]>

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Некорректная дата](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## GET /vendors/[vendorID]/recommended/stats/[stat]/download

Всё то же самое, что и у родительской ручки, кроме типа ответа.
В ответ приходит публично-доступная ссылка на CSV-файл с данными статистики.

### Дополнительные параметры
  - format `CSV|XLSX` - формат файла (по умолчанию CSV)

### Ответ
<[SimpleResponse](/_entities/responses/SimpleResponse.md) [[HtmlLink](/_entities/HtmlLink.md)]>