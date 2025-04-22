### Описание

Необходимо возвращать в ответе routestats данные, необходимые для передачи в inapp-communications.
Хотим в корень ответа добавить новое поле promo_context, в котором будет лежать информация, необходимая для промоплашек.
Плюсы: 
- возможность добавлять данные разного контекста (не только Драйва); 
- возможность поддержать идентичную схему в routestats и inapp-comm;
- возможность клиентам передавать контекст не вникая в детали, as is.

#### Почему именно в корень?
Хотим, чтобы у всех была возможность добавлять необходимую информацию в это поле. 
Альтернатива: сделать только для себя и прокидывать в drive_extra, но тогда мы ограничим тематику данных Драйвом.
Альтернатива 2: добавить поле promo_context в service levels, но тогда клиентам придется собирать контексты с каждого service level,
а хочется, чтобы клиент не парсил данные, а передавал as is.

Ранее обсуждалась возможность прокидывать данные не через клиента, а через кэш с использованием redis.
Раннее RFC: https://github.yandex-team.ru/taxi/rfc/pull/748
Для этого хотели заводить либу (сначала был сервис, но отказались), но после долгих обсуждений вернулись к малой крови.
Тикет на новый сервис (архревью в связанных) - st.yandex-team.ru/TAXIBACKEND-34577

### Пример ответа routestats с промо-оффером драйва для промоплашки
```json5
{
  "alternatives": {
    "options": []
  },
  "cache_estimated_waiting": {
    "distance": 100,
    "ttl": 30
  },
  "center_tab": true,
  "currency_rules": {
    "code": "RUB",
    "sign": "₽",
    "template": "$VALUE$ $SIGN$$CURRENCY$",
    "text": "руб."
  },
  "distance": "14 км",
  "jams": true,
  "notify": null,
  "offer": "50759186a63b547c1b0510654d46dbd6",
  "promo_context": {
    "drive_promo_offer_id": "8f5764c2-8b1e3954-ad3ed28b-24e4541b"
  },
  "service_levels": [],
  "time": "29 мин",
  "time_seconds": 1740,
  "typed_experiments": {
    "items": [],
    "version": 131751
  }
}


```

### Схема контекста
```yaml

PromoContext:
  type: object
  additionalProperties: false
  properties:
      drive_promo_offer_id:
          type: string
```
