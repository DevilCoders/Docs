# Отзывы на модели в кабинете вендоров.

## Внутренний стейт
`vendorsModelOpinions` - нормализованное хранилище в формате нормалайзера `{result: number[], entities: {user, modelOpinion, comment}}`

## GET `/vendors/<vendorId>/opinions`
Список отзывов на модели, поддерживает параметры:

  - from `<DateTime>(YYYY-DD-MM)` - левая граница фильтра по дате
  - to `<DateTime>(YYYY-DD-MM)` - правая граница фильтра по дате
  - grade `<Integer>` - фильтрация по оценке
  - withoutAnswer `<Boolean>` - только отзывы без ответа
  - onlyCpa `<Boolean>` - отзывы только проверенных покупателей
  - orderBy `<String>` - сортировка результата (`date` - по дате)
  - orderDirection `<String>` - направление сортировки (`asc`|`desc`)
  - [Параметры пагинации](https://github.yandex-team.ru/market/vendors-api-spec/blob/e9a84906af7704ccd7f45832e4a48a8154231fcf/_entities/Pager.md#Параметры)

[Ответ](https://github.yandex-team.ru/market/vendors-api-spec/blob/e9a84906af7704ccd7f45832e4a48a8154231fcf/vendors/%5BvendorId%5D/opinions/README.md#Ответ)

## GET `/vendors/<vendorId>/opinions/count`
Возвращает количество отзывов

[Ответ](https://github.yandex-team.ru/market/vendors-api-spec/blob/e9a84906af7704ccd7f45832e4a48a8154231fcf/vendors/%5BvendorId%5D/opinions/README.md#Ответ-1)

## POST `/vendors/<vendorId>/opinions/<opinionId>/comment`
Создание комментария к отзыву или комментарию на отзыв

### Данные
  - **text** `<String>` - текст комментария от вендора
  - [parentId] `<Number>` - идентификатор родительского комментария (если отвечаем на комментарий)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Number>` - идентификатор созданного комментария
  - errors `<Error[]>`

## PUT `/vendors/<vendorId>/opinions/<opinionId>/comment/<commentId>`
Изменение комментария к отзыву или комментарию на отзыв.

### Данные
  - **text** `<String>` - новый текст комментария.

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
  - **item** `<Boolean>` - признак успешности изменений
  - errors `<Error[]>`

## DELETE `/vendors/<vendorId>/opinions/<opinionId>/comment/<commentId>`
Удаление комментария к отзыву или комментарию на отзыв.

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Boolean>` - признак успешности удаления
  - errors `<Error[]>`

# Отчеты vendor yml раздела в кабинете вендоров

## Внутренний стейт
`vendorYmlReports` - часть стейта, хранящая отчеты

## GET `/vendors/<vendorId>/modelEdit/feeds/reports`
Возвращает отчеты

# Заявки

## Внутренний стейт
`vendorsEntries` - нормализованный стейт

## GET `/entries`

Получение списка заявок

- [Параметры](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/entries#%D0%9F%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B-1)
- [Ответ](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/entries#%D0%9E%D1%82%D0%B2%D0%B5%D1%82-1)


## POST `/entries`
Создание заявки

- [Параметры](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/entries#%D0%9F%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B)
- [Данные](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/entries#%D0%94%D0%B0%D0%BD%D0%BD%D1%8B%D0%B5)
- [Ответ](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/entries#%D0%9E%D1%82%D0%B2%D0%B5%D1%82)
