# Доступность Драйва в v1/availability

## Описание
Теперь в ручке доступности сервиса `superapp-misc` будет делаться
запрос в ручку Драйва для получения офферов.

Последовательность проверки:
1. Проверяем эксперимент `add_drive_cars`. Если пользователь не попадает
в эксперимент или эксперимент отключен — Драйв недоступен
2. Идем в ручку `/api/taxi/offers/standard` с параметрами:
* `src` — координаты пина (например, `src=37.52207773418206%2055.779502644746394`)
* `offer_count_limit` — лимит офферов (в нашем случае офферы не нужны, поэтому 0)
* `lang` — локаль пользователя
* `fast` — не учитывать пешие маршруты (чтобы запрос выполнялся быстрее)
Пример запроса:
POST `https://stable.carsharing.yandex.net/api/taxi/offers/standard?lang=ru&src=37.52207773418206%2055.779502644746394&offer_count_limit=0&fast=1`
3. Если в ответе `is_service_available=false` — Драйв недоступен
4. Если в ответе `reason_code=no_cars` — делаем кнопку серой

## Изменения в API
В `modes` и `products` появится новый объект с Драйвом.

`modes`:
```(json)
{
    "mode": "drive",
    "parameters": {
        "product_tag": "drive",
        "available": False,
        "show_disabled": True,
        "is_registered": True
    }
}
```

`products`:
```(json)
{"tag": "drive", "service": "drive", "title": "Drive"}
```
