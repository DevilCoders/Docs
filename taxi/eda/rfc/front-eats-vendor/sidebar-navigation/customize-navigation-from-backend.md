# Управление боковым меню в рестаппе с backend

### Цель:
управлять боковым меню в рестаппе без релиза фронта в зависимости от: ролей партнера, странаы, локали

### Полезные ссылки:
Продуктовый тикет: https://st.yandex-team.ru/EDAPRODUCT-3491

R&D тикет: https://st.yandex-team.ru/EDAPARTNERS-1739

Дизайн: https://www.figma.com/file/q2igigHZrjlPz7R0ils6M9/%D0%91%D0%BE%D0%BA%D0%BE%D0%B2%D0%BE%D0%B5-%D0%BC%D0%B5%D0%BD%D1%8E?node-id=1510%3A44578

### Решение:
1. Делаем новую ручку на бэке, которую будет дёргать фронт (раз в 3 минуты) при загрузке приложения (+ пуллинг). 
Ручка будет возвращать JSON c данными, необходимыми для рендеринга бокового меню (навигации).
2. Фронтенд обрабатывает данные из ручки и формирует компонтент react-router

### Список возможностей:
* различный порядок разделов и ссылок в меню
* скрытие и отображение произвольных разделов в меню в зависимости от настроек пользователя
* конфигурирования иконок
* конфигурирование бейджиков
* вывод подразделов меню
* вывод разделителей (текстовых)

### Схема ручки:
```yaml
openapi: 3.0.0
info:
    title: RestApp
    version: '1.0'

paths:
    /4.0/restapp-front/api/v1/configuration/navigation:
        get:
            description: Получение конфигрурации для отображения навигации / (бокового меню)
            parameters:
                - $ref: "#/components/parameters/PartnerId"
            responses:
                200:
                    description: OK
                    content:
                        application/json:
                            schema:
                                $ref: "#/components/schemas/NavigationResponse"

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

    schemas:
        NavigationResponse:
            type: object
            required:
                - logo
                - main
                - groups
            properties:
                logo:
                    description: Настройки логотипа
                    type: object
                    required:
                        - image
                    properties: 
                        image:
                            $ref: "#/components/schemas/LogoImage"
                main:
                    description: Настройки главной страницы
                    type: object
                    required:
                        - component
                    properties:
                        component:
                            $ref: "#/components/schemas/NavigationComponent"
                groups:
                    description: Группы навигации
                    type: array
                    items:
                        $ref: "#/components/schemas/NavigationGroup"
        LogoImage:
            description: Изображение для логотипа
            type: object
            required: 
                - path
            properties:
                path:
                    description: Путь/ссылка на изображение
                    type: string
                    example: https://eda.yandex/logo.svg
        NavigationGroup:
            description: Группа навигации
            type: object
            required:
                - id
                - nav
            properties:
                id:
                    type: string
                    description: Идентификатор группы навигации
                    example: main-navigation
                nav:
                    type: array
                    items:
                        $ref: "#/components/schemas/NavigationElement"

        NavigationElement:
            type: object
            required:
                - type
                - label
            properties:
                type:
                    description: "Тип элемента: component, iframe, separator"
                    type: string
                    example: component
                label:
                    description: Надпись (для отображения пользователю)
                    type: string
                    example: Главная страница
                title:
                    description: Текст для ховера
                    type: string
                    example: Текст подсказка
                children:
                    description: Дочерние элементы
                    type: array
                    items:
                        $ref: "#/components/schemas/NavigationElement"
                expanded:
                    description: Дочерние элементы раскрыты или нет
                    type: boolean
                    example: true
                icon:
                    $ref: "#/components/schemas/Icon"
                badge:
                    $ref: "#/components/schemas/Badge"
                component:
                    $ref: "#/components/schemas/NavigationComponent"
                link:
                    $ref: "#/components/schemas/NavigationLink"
                attributes:
                    $ref: "#/components/schemas/Attributes"

        NavigationLink:
            description: "Навигационная ссылка (для типов: iframe, link)"
            type: object
            required:
                - path
                - external
            properties:
                id:
                    description: Уникальный идентификатор
                    type: string
                    example: Restaurants
                path:
                    description: Путь / Ссылка
                    type: string
                    example: "https://ya.ru"
                external:
                    description: Внешняя ссылка или нет
                    type: boolean
                    example: true
                target:
                    description: Режим перехода по ссылке (открыть в новом окне)
                    type: string
                    default: self
                    enum:
                        - self
                        - blank
                attributes:
                    $ref: "#/components/schemas/Attributes"

        NavigationComponent:
            description: Компонент
            type: object
            required:
                - id
            properties:
                id:
                    description: Уникальный идентификатор (для маппинга c react)
                    type: string
                    example: Restaurants
                attributes:
                    $ref: "#/components/schemas/Attributes"

        Icon:
            description: Иконка
            type: object
            required:
                - name
            properties:
                name:
                    description: Название иконки
                    type: string
                    example: home
                title:
                    description: Текст для ховера
                    type: string
                    example: Текст подсказка
                attributes:
                    $ref: "#/components/schemas/Attributes"

        Badge:
            description: Бейджик
            type: object
            required:
                - type
            properties:
                id:
                    description: Уникальный идентификатор (для маппинга на react element)
                    type: string
                    example: MessagesCounter
                type:
                    description: "Тип бейджика: red-dot, counter, beta, new"
                    type: string
                    example: counter
                label:
                    description: Надпись (для отображения пользователю)
                    type: string
                    example: Новинка
                title:
                    description: Текст для ховера
                    type: string
                    example: Текст подсказка
                attributes:
                    $ref: "#/components/schemas/Attributes"

        Attributes:
            description: Дополнительные атрибуты
            type: object
            required:
                - attr
            properties:
                attr:
                    additionalProperties: true

```

### Пример ответа ручки:
```json
{
  "logo": {
    "image": {
      "path": "https://avatars.mds.yandex.net/get-bunker/118781/de823c1e8cf4526c4382b2ff9cd87affcbfe5991/svg"
    }
  },
  "main": {
    "component": {
      "id": "Statistics"
    }
  },
  "groups": [
    {
      "id": "main-navigation",
      "nav": [
        {
          "type": "component",
          "label": "Главная",
          "icon": {
            "name": "home"
          },
          "badge": {
            "type": "beta",
            "label": "Beta"
          },
          "component": {
            "id": "Statistics"
          }
        },
        {
          "type": "component",
          "label": "Рестораны",
          "icon": {
            "name": "kiosk"
          },
          "component": {
            "id": "Restaurants"
          }
        },
        {
          "type": "page",
          "label": "Меню",
          "icon": {
            "name": "blank"
          },
          "badge": {
            "id": "MenuDeclined",
            "type": "red-dot"
          },
          "component": {
            "id": "Menu"
          }
        }
      ]
    },
    {
      "id": "bottom-navigation",
      "nav": [
        {
          "type": "iframe",
          "label": "База знаний",
          "link": {
            "path": "https://vendor.eda.yandex/support/index",
            "external": true
          }
        },
        {
          "type": "link",
          "label": "Выход",
          "link": {
            "path": "/logout",
            "external": false
          }
        }
      ]
    }
  ]
}
```