# Рекомендации ставок

Сейчас партнеры сами выставляют себе ставки за показы, рискуя следующим образом:
- ставка слишком маленькая -> мало или вообще нет показов
- ставка слишком высокая -> много показов, но неоправданно большие траты
- управление аукционом с нашей стороны
- упрощение заведения рекламы для партнеров
При помощи рекомендации оптимальной ставки хотим увеличить количество показов и уменьшить финансовые вливания партнеров в рекламу.

## Содержание

1. [Формируем табличку в yt](#yt-table)
2. [Храненим рекомендованные значения в сервисе](#service-table)
3. [При создании кампании дергаем ручку budget-recommender](#budget-recommender)
4. [При отображении списка кампаний смотрим рекомендации](#campaigns-list)
6. [Поведение на фронте](#front)

<a id="yt-table"></a>

## Табличка в yt со схемой:

```yaml
place_id:
    type: integer
    format: int64_t
wins_percent: 
    type: int
weekly_spend_limit:
    type: integer
    format: int64_t
average_cpc: 
    type: integer
    format: int64_t
```

<a id="service-table"></a>

## Хранение рекомендованных значений

Кэш над табличкой в yt

<a id="budget-recommender"></a>

## Ручка, отдающая рекомендованую ставку

```yaml
/4.0/restapp-front/marketing/v1/ad/budget-recommender:
    get:
        parameters:
              - name: place_ids
                in: query
                required: false
                        type: integer
                        format: int64
        responses:
                200:
                    content:
                        application/json:
                            schema:
                                    type: array
                                    description: только n рекомендаций
                                    items:
                                        type: object
                                        additionalProperties: false
                                        required:
                                            - percent
                                        properties:
                                            percent: "#/components/schemas/Percent"
                                            week_budget: "#/components/schemas/Money"
                                            bid: "#/components/schemas/Money"


```
+ конфиг с количеством ставок, чтобы выводить не больше, чем нужно по дизайну.

<a id="campaigns-list"></a>

## Расширение ручки списка кампаний
Добавляем массив рекомендаций в список плейсов.
```yaml
...
recommendations:
type: array
    items:
        type: object
        additionalProperties: false
        required:
        - percent
        properties:
            percent: "#/components/schemas/Percent"
            week_budget: "#/components/schemas/Money"
            bid: "#/components/schemas/Money"
...
```
<a id="front"></a>

## Фронт

Если ручка возвращает непустой массив - отрисовываем рекомендации в ручке создания и редактирования.
Подсвечиваем ставки, которые не соответствуют рекомендациям, отображаем рекомендованные ставки при наведении.
