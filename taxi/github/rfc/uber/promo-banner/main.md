# Промо банер в поездке [draft]

Какие проблемы хотим решить:
1. Закрепить устовшийся способ промотирования на экране поездки в Uber в протоколе
2. Уметь на основе данных о заказе принимать решение о промотировании

## API

```yaml
Background:
    description: Медиа для клиента, полученное по MediaTag в соответствии с MediaSizeInfo
        клиента
    type: object
    properties:
        type:
            description: Тип медиа - image, video...
            type: string
        content:
            description: Ссылка, обычно на s3-promotions
            type: string
        thumbnail:
            type: string
        loop:
            type: boolean
    required:
      - type
      - content
    additionalProperties: false
      
Banner:
    type: object
    properties:
        id:
            type: string
        title:
            type: object
            properties:
                items:
                    $ref: '#/definitions/AttributedText'
            additionalProperties: false
            required:
              - items
        text:
            type: object
            properties:
                items:
                    $ref: '#/definitions/AttributedText'
            additionalProperties: false
            required:
              - items
        icon:
            type: object
            description: |
                Картинка в правой части баннера
            properties:
                image_tag:
                    type: string
                image_url:
                    type: string
            additionalProperties: false
        background:
            $ref: '#/definitions/Background'
        action:
            type: object
            description: |
                Базовое действие выполняемое по нажатию на банер
            properties:
                deeplink:
                    type: string
        show_policy:
            type: object
            description: |
                Информация о политике показа промоблока: количество показов, количество переходов и т.д.
            properties:
                id: 
                    type: string
                    description: Идентификатор счётчика
                max_show_count:
                    type: integer
                    minimum: 0
                max_widget_usage_count:
                    type: integer
                    minimum: 0
            additionalProperties: false
            required:
              - id
              - max_show_count
              - max_widget_usage_count
    additionalProperties: false
    required:
      - id
      - title

BannersOnTheWay:
    type: object
    properties:
        items:
            type: array
            description: Список банеров, отсортированных по приоритету показа
            iterms:
                $ref: '#/definitions/Banner'

TotwStories:
    descrition: Текущий объект сторис, который отдается в Go

PromosOnTheWayRequest:
    type: object
    description: АПИ на усмотрение разрабочика, но нужно учесть что поля будут расширяться какими-то данными из заказа
    properties:
        tariff_class:
            type: string
        point_a:
            $ref: "inapp-communications/definitions.yaml#/definitions/PointGeometry"
        point_b:
            $ref: "inapp-communications/definitions.yaml#/definitions/PointGeometry"
    required:
        - point_a
        - tariff_class
    additionalProperties: false

PromosOnTheWayResponse:
    type: object
    description: ответ ручки v1/promos-on-the-way. Запрос будет 
    properties:
        stories:
            $ref: 'TotwStories'
        promotions:
            $ref: 'BannerOnTheWay'

TotwResponse:
    type: object
    properties:
        promotions:
          description: Новая структура промо объектов
          type: object
          properties:
              banners: 
                $ref: '#/definitions/BannersOnTheWay'
        # other fieles from totw here
    additionalProperties: false
    required:
      - promotions
```

## Клиентская логика:

1. Получаем в totw список банеров для показа
2. Выбираем подходящий банер в зависимости от show_policy
3. Отправляем в апметрику сигнал о выбранном банере
4. Показываем банер

Как выбрать подходящий банер для показа:
1. Ищем первый банер, который удовлетворяет условием показа по show_policy.
2. После того как текущий банер выполнил условия показа, показываем следующий подходящий из списка, если список закончился - ничего не показываем

## Backend

### Архитекутура
![](https://jing.yandex-team.ru/files/ulturgashev/arch.jpg "Архитектура взаимодействия")

### Требование к новому типу промо-объектов
Хотелось бы видеть наличие следующих полей:
- Приоритет
- Заголовок
- Текст
- Show policy(id счетчика, лимит показов и лимит нажатий)
- Бэкграунд
- Action
- Раскатка через эксп по consumer (для банеров, стоит завести отдельный consumer)

### План работы
- Добавляем новый тип промок `banner_on_the_way`. Доработки `/admin/promotions/create` + `/internal/promotions/list`
- Реализация фронта для нового типа промки (Завести задачу на фронт, фронт делает https://staff.yandex-team.ru/eol95)
- Правки в кэше `inapp-communications` - добавляем новый тип промок
- Создаём новую ручку `v1/promos-on-the-way`, переносим туда формирование `promotions`(банеры убера + старые сторисы)
- Правки на стороне API-PROXY, переезд на новую ручку c сохранением правил кэширования
- Удаление ручки `/4.0/totw-stories`

Развитие ручки:
- В будущем, в зависимости от требований промотирования, у ручки, появится зависимость от `order-core`. Вызов ручки будет дожидаться ответа `order-core` для запроса.
