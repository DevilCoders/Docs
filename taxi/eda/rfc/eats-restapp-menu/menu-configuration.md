# Получение конфигурации меню

### Цель:

в зависимости от: страны ресторана, локали партнера, типа бизнеса бренда выдавать настройки меню (конфигурацию)

### Полезные ссылки:

R&D тикет: https://st.yandex-team.ru/EDAPARTNERS-1870

### Решение:

1. Делаем новую ручку на бэке, которую будет опрашивать фронт при загрузке меню.
   Ручка будет возвращать JSON с настройками: списком стандартных категорий, в дальнейшем и другие настройки (список
   НДС, и т.п.)
2. Фронтенд передаёт в ручку параметры: place_id, заголовок с локалью.
3. Формируем кварги и передаём в конфиг-эксперимент 3.0, который возвращает наборы категорий в зависимости от кваргов.
   (или/и ходит в другие конфиги за настройками стран)

### Список возможностей:

* различный список категорий меню для разных стран (напр. в Армении можно доставлять алкоголь)
* локализация названий стандартных категорий меню
* различный список категорий меню для разных типов бизнеса
* вывод дополнительных параметром для отображения и управления меню

### Параметры

#### Заголовки

- ``X-Language`` - Локаль выбранная пользователем (из куки)

#### Query параметры

- ``place_id`` - идентификатор заведения

### Схема ручки:

```yaml
openapi: 3.0.0
info:
    title: RestApp
    version: '1.0'

paths:
    /4.0/restapp-front/eats-restapp-menu/v1/configuration:
        get:
            description: Получение конфигрурации меню
            parameters:
                -   $ref: "#/components/parameters/PartnerId"
                -   $ref: "#/components/parameters/XLanguage"
                -   $ref: "#/components/parameters/PlaceId"
            responses:
                200:
                    description: OK
                    content:
                        application/json:
                            schema:
                                $ref: "#/components/schemas/Response"

components:
    parameters:
        PartnerId:
            name: X-YaEda-PartnerId
            in: header
            required: true
            description: ID партнера
            schema:
                type: integer
                format: int64
        XLanguage:
            name: X-Language
            in: header
            required: true
            description: Локаль
            schema:
                type: string
                default: ru
        PlaceId:
            name: place_id
            in: query
            required: false
            description: Идентификатор заведения
            schema:
                type: integer
                format: int64

    schemas:
        Response:
            type: object
            required:
                - categories
            properties:
                categories:
                    description: Настройки категорий
                    type: object
                    required:
                        - standard
                    properties:
                        standard:
                            type: object
                            description: Стандартные категории
                            required:
                                - list
                            properties:
                                list:
                                    description: Список категорий
                                    type: array
                                    items:
                                        $ref: "#/components/schemas/Category"
                                configuration:
                                    $ref: "#/components/schemas/Configuration"
                        custom:
                            type: object
                            description: Пользовательские категории
                            properties:
                                configuration:
                                    $ref: "#/components/schemas/Configuration"
        Category:
            type: object
            description: Категория меню
            required:
                - name
                - origin_id
            properties:
                name:
                    type: string
                    description: Название категории
                    example: Бургеры
                origin_id:
                    type: string
                    description: Идентификатор категории
                    example: "2cbcefe3-8857-4376-99bc-9833b57cf25d"
        Configuration:
            type: object
            description: Настройки категорий
            properties:
                min:
                    type: integer
                    description: Минимальное количество категорий
                    minimum: 0
                max:
                    type: integer
                    description: Максимальное количество категорий
                    minimum: 0

```

### Пример ответа ручки:

```json
{
  "categories": {
    "standard": {
      "list": [
        {
          "name": "Салаты",
          "origin_id": "2cbcefe3-8857-4376-99bc-9833b57cf25d"
        },
        {
          "name": "Бургеры",
          "origin_id": "2cbcefe3-8857-4376-99bc-9833b57cf25d"
        }
      ]
    },
    "custom": {
      "configuration": {
        "max": 3
      }
    }
  }
}
```