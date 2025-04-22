# Передавать причину получения промокода
Постановка задачи: https://st.yandex-team.ru/TAXIBACKEND-31242

## Вводная
Необходимо для некоторых промокодов возвращать причину их получения.

На фронт промокоды приходят в ответе ручки coupons/list в виде массива объектов [Coupon](https://github.yandex-team.ru/taxi/uservices/blob/356333429634db981033a3781511cf8229602d02/services/coupons/docs/yaml/definitions.yaml#L321)
В коде ручки сначала для пользователя из монго коллекции user_coupons достаются все промокоды (сами коды строками) пользователя, после чего во время валидации из монго коллекции promocodes получается дополнительная информация о каждом промокоде и на основе её и результата проверки составляется ответ со списком объектов Coupon.

Промокоды в promocodes добавляются разными способами. Нас интересуют промокоды в награду за рефералку, они добавляются ручкой internal/generate. Ручка дёргается из stq таски referral_gen_reward



## Решение

### Коллекция promocodes
Добавляем необязательное поле reason. Для локализуемости это будет объект танкерный ключ + аргументы.

```yaml
...
reason:
  type: object
  additionalProperties: false
  properties:
    default:
      type: string
    tanker_key:
      type: string
    tanker_args:
      type: array
      items:
        type: object
        additionalProperties: false
        properties:
            key:
              type: string
            value:
              type: string
          required:
            - key
            - value
    required:
      - default
      - tanker_key
...

```

### Ручка coupons/list
Изменение в api ответа.
Добавить в возращаемый объект [Coupon](https://github.yandex-team.ru/taxi/uservices/blob/356333429634db981033a3781511cf8229602d02/services/coupons/docs/yaml/definitions.yaml#L321) необязательное строковое поле subtitle (Coupon в ответе list выглядит [так](https://github.yandex-team.ru/taxi/uservices/blob/356333429634db981033a3781511cf8229602d02/services/coupons/docs/yaml/api/coupons_list.yaml#L86)).
```yaml
...
subtitle:
    type: string
...

```
Заполнять его из поля reason коллекции promocodes, после перевода в танкере.

### Ручка internal/generate
Добавить в запрос необязательное поле reason, схема как в коллекции promocodes. Записывать его в коллекцию.

### Stq таска referral_gen_reward
Вызывать generate с заполненным полем reason. Значение танкерного ключа и аргументов reason для сценария "промокод в награду за рефералку" можно завдавать через конфиг.

### Оценка
1. internal/generate 0.5d
1. referral_gen_reward 0.5d
1. coupons/list 1d

Итого 2d
