# Кешбек за мастеркард

Хотим вместо скидки начать выдавать кешбек

Дизайн (подпись под способом оплаты не делаем) https://www.figma.com/file/zWSt3vNWyrVQPQYX7YI23B/Go-%D0%9F%D0%BB%D1%8E%D1%81?node-id=38957%3A1712 

<img src="./imgs/design.png" width="900">


В догонку пример как хочется чтобы работало:

```
кейс 1: у пользователя есть кешбэк плюс и скидка мастеркард
- изначальная стоимость поездки 1000р
- сначала применяется правило мастеркарда и скидка с него (15% например)
- цена стала 850р
- теперь применяем агентский кешбэк такси
- стало 850р + 85 кешбэка

кейс 2: у пользователя есть кешбэк плюс и кешбэк мастеркард
- изначальная стоимость поездки 1000р
- сначала применяется правило мастеркарда и кешбэк (15% например)
- цена стала 1000р и 150р кешбэак
- теперь применяем агентский кешбэк такси
- стало 1000р и 150 +100 кешбэка
```

## Небольшие вводные по тому как сейчас работает мастеркард

Скидка мастеркард заводится через сервис скидок, вот пример https://tariff-editor.taxi.yandex-team.ru/discounts2/user/show/moscow/bbf9bba2-2566-41e8-b557-e5cca97894d6

в большинстве случаев она работает как и любая другая скидка но есть несколько отличий:
В zone-info для скидки мастеркард заводится специальный брендинг c иконкой (есть еще отдельный брендинг для плюсовых)

```
{
    "card": {
        "badge_icon": {
            "size_hint": 240,
            "url": "https://tc.mobile.yandex.net/static/images/10593/92bb2211d2284bf8b74fe59e0d668278",
            "url_parts": {
                "key": "TC",
                "path": "/static/images/10593/92bb2211d2284bf8b74fe59e0d668278"
            }
        },
        "badge_subtitle": "скидка от Mastercard",
        "badge_title": "Скидка"
    },
    "name": "",
    "type": "mastercard"
}
```


Для плюсовиков:

```
{
    "brand_color": "#357AFF",
    "card": {
        "badge_icon": {
            "size_hint": 240,
            "url": "https://tc.mobile.yandex.net/static/images/11896/678c9c80d2da485da028a31456dbe096",
            "url_parts": {
                "key": "TC",
                "path": "/static/images/11896/678c9c80d2da485da028a31456dbe096"
            }
        },
        "badge_subtitle": "от Плюс и Mastercard",
        "badge_title": "Скидка на поездки"
    },
    "icon": {
        "size_hint": 240,
        "url": "https://tc.mobile.yandex.net/static/images/38221/4cebcfafd3084ca9adf239b82913fc26",
        "url_parts": {
            "key": "TC",
            "path": "/static/images/38221/4cebcfafd3084ca9adf239b82913fc26"
        }
    },
    "inactive_icon": {
        "size_hint": 240,
        "url": "https://tc.mobile.yandex.net/static/images/10005/ea831da72241463a8844c5e0ee1354be",
        "url_parts": {
            "key": "TC",
            "path": "/static/images/10005/ea831da72241463a8844c5e0ee1354be"
        }
    },
    "name": "",
    "type": "ya_plus_mastercard"
}
```

который отображается в карточке заказа, если в routestats в service_classes.discount пришло поле mastercard (или ya_plus_mastercard)

<img src="./imgs/mastercard_branding.png" width="400">


отсюда следует несколько выводов:
* Нужно различать кешбечный мастеркард от некешбечного и возвращать в routestats другой discount, в случае кешбека
* Заводить отдельный брендинг в zoneinfo для кешбек мастеркарда, кажется это не первоочередная задача можно унести за рамки MVP


## Основная часть

### Бейдж в zoneinfo (вне MVP)

Предлагается сохранить точно такую же структуру, как и была ранее и в ответе zoneinfo возвращать новый брендинг следующего вида (и аналогичный для плюсовых пользователей)

```
{
    "card": {
        "badge_icon": {
            "size_hint": 240,
            "url": "https://tc.mobile.yandex.net/static/images/10593/92bb2211d2284bf8b74fe59e0d668278",
            "url_parts": {
                "key": "TC",
                "path": "/static/images/10593/92bb2211d2284bf8b74fe59e0d668278"
            }
        },
        "badge_subtitle": "от Mastercard",
        "badge_title": "Кешбек за поездки"
    },
    "name": "",
    "type": "mastercard_cashback"
}
```


В routestats возвращать в service_classes.discount значение mastercard_cashback


### Брендинги в routestats


По условию скидка за мастеркард может быть: двойной, тройной, ... (n-ной), для этого в routestats необходимо научиться различать тип мастеркардовой скидки (сейчас мастеркардовская скидка определяется по условию, что скидка по бинам и эти бины принадлежат мастеркарду).
Для этого предлагается в сервис скидок добавить новый параметр discount_tag (нужны доработки на фронте и в админке заведения скидок), этот параметр будет возвращаться в ответе /v3/get-discount,  


Пример:
```
{
  "discount_offer_id": "60252686b35f4d6c4873635b",
  "discounts": {
    "business": {
      "calc_data": [
        {
          "coeff": 10,
          "price": 100
        },
        {
          "coeff": 20,
          "price": 200
        }
      ],
      "calc_type": "table",
      "discount_info": {
        "description": "Cashback", // не хочу на эту штуку завязываться
        "discount_id": "4adcf380-e2ac-483f-90b4-388996e0eb98",
        "is_price_strikethrough": true,
        "limited_rides": false,
        "method": "subvention-fix",
        "reason": "for_all"


        "discount_tag": "mastercard_triple_cashback",  // пока еще думаю над крутым названием тега


      },
      "is_cashback": true,
      "restrictions": {
        "driver_less_coeff": 1,
        "max_absolute_value": 100,
        "max_discount_coeff": 0.99,
        "min_discount_coeff": 0.01,
        "payment_type": "card",
        "recalc_type": "none"
      }
    }
  }
}
```


внутри routestats будет формироваться 2 брендинга мастеркарда: один для плашки, другой для карточки тарифа, если discount_tag будет присуствовать в конфиге 

пример структуры конфига

```
{
    "mastercard_triple_cashback": {
        "push_title": "some_tanker_key", // надо подумать насколько будет сложно резолвить нормальные названия тарифов типо "В комфорт двойной кешбек баллами"
        "push_subtitle": "some_tanker_key", // предлагаю прямо в танкерном ключе хардкодить "10% от мастеркарда, 10% от плюса"
        "title": "another tanker key" // ключ для карточки заказа
        "subtitle": "another tanker key" // ключ для карточки заказа
        "banner_id": "идентификатор коммуникации"
        "image_tag": "mastercard_img" // иконка, которую возвращаем в брендинге
    }
}
```



пример результирующего брендинга для плашки:
```
{
    "brandings": [
        {
            "title": "В Ultima двойной кешбек баллами",
            "subtitle": "10% от Mastercard, 10% от Плюса"
            "type": "mastercard_cashback_notification",
            "extra": {
                "banner_id": "id",
            },
            "image_tag": "image_tag",
            "action": "show_banner"
        },
    ]
}
```


Пример брендинга для карточки тарифа. Тут предлагается модифицировать уже существующий брендинг cashback
```
{
    "brandings": [
        {
            "title": "Двойной кешбек баллами",
            "subtitle": "Mastercard 10%, Плюс 10%"
            "type": "cashback",
            "extra": {
                "banner_id": "id",
            },
            "value": 42,
            "action": "show_banner"
        },
    ]
}
```

Какие вопросы еще остались:
* ~~Как резолвить имя тарифа в заголовке плашки от мастеркарда~~. Не актуально, текст поменяют


### Преобразования скидки Mastercard и совместимость с плюсом

Если прямо сейчас переключить скидку на кешбечный вариант (поставить галку is_cashback=True), то скидка заработает, но не во всех кейсах. Сейчас есть несколько преобразований прайсинга для начисления маркетингого кешбека, например такое https://tariff-editor.taxi.yandex-team.ru/price-conversion-rules/view/712?view=list

В результате работы такого преобразования в мету множителя кешбека запишется последнее оработанное преобразование, т.е. фактически кешбечная скидка за мастеркард может перетереться маркетинговым кешбеком на бизнес. В качестве варианта решения предлагается объединить преобразования в одно преобразование.


#### Отображение кешбека на экране с плюсом

Проверил в тестинге, кешбек заведенный через скидку суммируется в офере routestats и в конце поездки, в current_prices лежат корректные цены за плюсовый кешбек и за скидочный кешбек


Место в routestats с суммированием https://github.yandex-team.ru/taxi/backend-cpp/blob/b0531d792ce720a02f7bd9f298497e99db223621/protocol/lib/src/views/routestats/brandings/builders.cpp#L51

заказ на котором проверял https://tariff-editor.taxi.tst.yandex-team.ru/orders/c411c9701da25dd4bdbe8b5a8918d0be/raw-objects?phone_type=all&phone=%2B79960452712

структука current_prices в конце поездки

```
    "current_prices": {
      "cashback_price": 38,
      "kind": "final_cost",
      "user_ride_display_price": 377,
      "user_total_display_price": 377,
      "user_total_price": 377,
      "cost_breakdown": [
        {
          "type": "card",
          "amount": 377
        }
      ],
      "discount_cashback": 67
    },
```

<img src="./imgs/totw.png" width="400"><img src="./imgs/routestats.png" width="400">



## Скоуп

MVP:
* Пробросить поле discount_tag через админку скидок (2 дня)
* Возвращать discount_tag в ответе /v3/get-discount (1 день)
* Формировать брендинги в routestats (в новом routestats судя по всему) (3 дня)
* Возвращать для кешбечной мастеркардовой скидки discount = mastercard_cashback (переопределяем в новом routestats) (2 дня)
* Объединить преобразования маркетингого кешбека в одно (примерно вечность =) )



Доп фичи:
* Формировать новый брендинг mastercard_cashback в zoneinfo



## Как мы режем скоуп

У проекта есть дедлайн первого марта, а со скидками пока нет возможности согласовать изменения, поэтому предлагается следующее временное решение вместо добавления нового поля в сервис скидок.


1) Двойные, тройный и тд скидки это все разные скидки в сервисе скидок
2) Из ручки get-discount помимо основной информации по скидке получается еще название скидки в поле description


предлагается определять тип скидки при помощи поля description из скидки, для этого заведем временный отдельный конфиг 
```
{
    "rosbank_yt_mastercard_ru_31_08_2020": "mastercard_triple_cashback"
}
```

по которому будем определять тип скидки


Итоговый скоуп:
* Формировать брендинг-плашку для кешбечного мастеркарда  
* Дополнять брендинг cashback есть пришла кешбечная скидка мастеркарда
* Возвращать в поле discount = other если пришла кешбечная скидка мастеркарда
