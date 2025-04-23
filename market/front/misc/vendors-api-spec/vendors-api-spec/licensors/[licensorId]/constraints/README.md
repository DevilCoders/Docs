# Ресурс /licensors/[licensorId]/constraints

## GET /licensors/[licensorId]/constraints

Возвращает список ограничений на маркетные бренды и категории, установленные для заданного лицензиара 

### Примечания
  - Ручка доступна обоим менеджерам, суппорту и всем ролям лицензиара
  - Для нераспознанного (несматченного, неформализованного) лицензиара возвращает пустой набор ограничений

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Array[Object]>` - список ограничений лицензиара, где ограничение описывается следующей структурой:
      - **licensorMarketId** `<Integer>` - маркетный айдишник лицензиара, прописанный в МБО 
      - **brand** [`<Brand>`](/_entities/Brand.md) - бренд для ограничения
      - **category** [`<Category>`](/_entities/Category.md) - категория для ограничения
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого лицензиара](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)

## POST /licensors/[licensorId]/constraints/[brandId]/[categoryId]

Устанавливает одно ограничение на маркетный бренд и категорию для заданного лицензиара

### Примечания
   - Ручка доступна менеджеру, суппорту и всем ролям лицензиара
   - Ручка идемпотентна: при повторном вызове с одинаковыми входными данными дубликата связи не создаст и вернет true

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  
### Переменные пути
  - **licensorId** `<Integer>` - айдишник лицензиара, выданый в КВ
  - **brandId** `<Integer>` - маркетный айдишник бренда, прописанный в МБО 
  - **categoryId** `<Integer>` - маркетный айдишник категории, прописанный в МБО 

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
        - **status** `<Boolean>` - если ограничение успешно установлено или уже существовало, то вернет true, в противном случае прилетит ошибка
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого лицензиара](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Некорректное значение brandId (brand with id ${brandId} doesn't exist)](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Некорректное значение categoryId (category with id ${categoryId} doesn't exist)](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
 
#### Лицензиар не распознан (неформализован, несматчен)
  - statusCode: `400`
  - code: `NOT_RECOGNIZED_LICENSOR`
  - message: `licensor ${licensorId} is not recognized (no corresponded market id from MBO matched)`
  
## DELETE /licensors/[licensorId]/constraints/[brandId]/[categoryId]

Удаляет одно ограничение на маркетный бренд и категорию для заданного лицензиара

### Примечания
   - Ручка доступна менеджеру, суппорту и всем ролям лицензиара
   - Ручка идемпотентна: при повторном вызове с одинаковыми входными данными вернет true

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  
### Переменные пути
  - **licensorId** `<Integer>` - айдишник лицензиара, выданый в КВ
  - **brandId** `<Integer>` - маркетный айдишник бренда, прописанный в МБО 
  - **categoryId** `<Integer>` - маркетный айдишник категории, прописанный в МБО 

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
        - **status** `<Boolean>` - если ограничение успешно удалено или не существует, то вернет true, в противном случае прилетит ошибка
  - errors `<Error[]>`
  
### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого лицензиара](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Некорректное значение brandId (brand with id ${brandId} doesn't exist)](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Некорректное значение categoryId (category with id ${categoryId} doesn't exist)](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
 
#### Лицензиар не распознан (неформализован, несматчен)
  - statusCode: `400`
  - code: `NOT_RECOGNIZED_LICENSOR`
  - message: `licensor ${licensorId} is not recognized (no corresponded market id from MBO matched)`
