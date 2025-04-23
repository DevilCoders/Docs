# Продуктовое описание

Увеличиваем поиск машины, чтобы найти машину ближе к пользователю и оптимизировать подачу, и снижаем долю отмен за счет правильной коммуникации с пользователем на этапе поиска в продукте.

[Tracker](https://st.yandex-team.ru/TAXIPROJECTS-2830)

[Figma](https://www.figma.com/file/XOZTS4jHddktQcEdkzJa9D/Долгий-поиск?node-id=1477%3A41935)

[Miro](https://miro.com/app/board/o9J_lhjSTB8=/)

## API и логика
1. После создания заказа клиент начинает периодически поллить ручку

```json
/4.0/order-search-status/v1/long-search-info:
  get:
      parameters:
        - in: query
          description: Идентификатор заказа
          name: order_id
          schema:
              type: string
          required: true
      responses:
          200:
              description: OK
              $ref: 'LongSearchInfoResponse'
          404:
              $ref: 'Error'
          500:
              $ref: 'Error'

DriverPosition:
    description: |
        Информация о позиции водителя на карте
    additionalProperties: false
    type: object
    required:
      - lon
      - lat
      - direction
      - timestamp
    properties:
        lon:
            type: number
        lat:
            type: number
        speed:
            type: number
        direction:
            type: number
        timestamp:
            type: string

LongSearchInfoResponse:
    additionalProperties: false
    type: object
    properties:
        radius:
            description: |
                Текущий радиус для отображения на экране поиска (в метрах)
            type: integer
            minimum: 1
        eta:
            description: |
                Текущий eta для отображения на экране поиска (в секундах)
                Может отсутствовать, когда в самом начале нет кандидата.
                Либо если показ eta в отстутствии кандадата прикрыт конфигом.
            type: integer
            minimum: 1
            x-taxi-cpp-type: std::chrono::seconds
        performer:
            description: |
                Информация о текущем кандидате на заказ.
                Если пустое, то кандидат еще не найден, либо предыдущий кандидат отказался
            additionalProperties: false
            type: object
            properties:
                id:
                    description: Идентификатор кандидата
                    type: string
                display_tariff:
                    description: Отображаемый тариф
                    type: string
                    example: 'econom'
                positions:
                    description: Последние позиции водителя на карте
                    type: array
                    items:
                        $ref: 'DriverPosition'
            required:
              - id
              - display_tariff
              - positions
        hints:
            additionalProperties: false
            type: object
            properties:
                search_status:
                    description: |
                        Локализованная подсказка о статусе поиска
                    type: string
            required:
              - search_status
    required:
      - radius
      - hints

Error:
    description: Error response
    type: object
    additionalProperties: false
    properties:
        message:
            description: Человекочитаемая ошибка
            type: string
        code:
            description: Код ошибки
            type: string
    required:
      - message
      - code
```
