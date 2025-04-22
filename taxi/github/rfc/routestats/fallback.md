# Фолбэк routestats
<!-- MarkdownTOC autolink="true" -->

- [TL; DR](#tl-dr)
- [Мотивация фолбэка](#%D0%9C%D0%BE%D1%82%D0%B8%D0%B2%D0%B0%D1%86%D0%B8%D1%8F-%D1%84%D0%BE%D0%BB%D0%B1%D1%8D%D0%BA%D0%B0)
- [Фолбэк в общих чертах](#%D0%A4%D0%BE%D0%BB%D0%B1%D1%8D%D0%BA-%D0%B2-%D0%BE%D0%B1%D1%89%D0%B8%D1%85-%D1%87%D0%B5%D1%80%D1%82%D0%B0%D1%85)
  - [Фолбэк. Схема подключения](#%D0%A4%D0%BE%D0%BB%D0%B1%D1%8D%D0%BA-%D0%A1%D1%85%D0%B5%D0%BC%D0%B0-%D0%BF%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D1%8F)
  - [Фолбэк. Протокол ответа](#%D0%A4%D0%BE%D0%BB%D0%B1%D1%8D%D0%BA-%D0%9F%D1%80%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BB-%D0%BE%D1%82%D0%B2%D0%B5%D1%82%D0%B0)
    - [Пример рабочего ответа фолбэка](#%D0%9F%D1%80%D0%B8%D0%BC%D0%B5%D1%80-%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE-%D0%BE%D1%82%D0%B2%D0%B5%D1%82%D0%B0-%D1%84%D0%BE%D0%BB%D0%B1%D1%8D%D0%BA%D0%B0)
  - [Фолбэк. Как решаем surgeprice](#%D0%A4%D0%BE%D0%BB%D0%B1%D1%8D%D0%BA-%D0%9A%D0%B0%D0%BA-%D1%80%D0%B5%D1%88%D0%B0%D0%B5%D0%BC-surgeprice)
  - [Фолбэк. Как регистрировать пины](#%D0%A4%D0%BE%D0%BB%D0%B1%D1%8D%D0%BA-%D0%9A%D0%B0%D0%BA-%D1%80%D0%B5%D0%B3%D0%B8%D1%81%D1%82%D1%80%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D1%82%D1%8C-%D0%BF%D0%B8%D0%BD%D1%8B)
- [Фолбэк. Саммари \(Big picture\)](#%D0%A4%D0%BE%D0%BB%D0%B1%D1%8D%D0%BA-%D0%A1%D0%B0%D0%BC%D0%BC%D0%B0%D1%80%D0%B8-big-picture)
- [Как включаем](#%D0%9A%D0%B0%D0%BA-%D0%B2%D0%BA%D0%BB%D1%8E%D1%87%D0%B0%D0%B5%D0%BC)
- [На уровне кода](#%D0%9D%D0%B0-%D1%83%D1%80%D0%BE%D0%B2%D0%BD%D0%B5-%D0%BA%D0%BE%D0%B4%D0%B0)
- [Ожидаемый результат](#%D0%9E%D0%B6%D0%B8%D0%B4%D0%B0%D0%B5%D0%BC%D1%8B%D0%B9-%D1%80%D0%B5%D0%B7%D1%83%D0%BB%D1%8C%D1%82%D0%B0%D1%82)
- [Скоуп работ](#%D0%A1%D0%BA%D0%BE%D1%83%D0%BF-%D1%80%D0%B0%D0%B1%D0%BE%D1%82)

<!-- /MarkdownTOC -->

## TL; DR

Включение фолбэка routestats должно скрыть от пользователя факт проблем в сервисе и увеличить конверсию в заказ

side-by-side сравнение

![video](https://jing.yandex-team.ru/files/rgnlax/side-by-side_s4yy3bYV_x6Vd.mov)

Горение заказов surgeprice:

![img](https://jing.yandex-team.ru/files/rgnlax/Screenshot%202020-10-19%20at%2011.15.02.png)

По сравнению с обычным четвергом, в факапочный четверг сгорело +2000 заказов из-за surgeprice.

https://datalens.yandex-team.ru/preview/gxzm6fbeec3ub

### Метод расчета

15 октября был факап. В момент факапа 2k rps routestast срезалось рейтлимитером.
В этом момент приложение выглядело как на видео. Юзеры, которые не повезло остались без routestats вовсе и пошли в заказ.

Так как в этот момент был сурдж, сервис не искал водителей пока юзер явно не окнет сурдж. Многие юзеры так и не окнули и заказы перешли в expired

По сравнению с обычным четвергом +2000 заказов.

## Мотивация фолбэка

Несмотря на то, что routestats необязательная ручка для цикла заказа, без ее ответа интерфейс приложения выглядит неполным.

Ситуация усугубляется также тем, что когда в зоне А есть сурдж (во время факапов почти всегда), без ответа routestast будет surgeprice.
Surgeprice -- не ищем водителя, пока юзер явно не окнет сурдж.

Ошибку routestats клиентское приложение отказывается принимать и ретраит routestats до победы. Это приводит к повышенной нагрузке на монолит backend-cpp, то есть монолит не поднимается и юзеры не могут заказать такси.
Рейтлимитер частично решает проблему с нагрузкой на монолит, и никак не решает проблему интерфейса. На последнем факапе (2000 rpss 5xx в routestats).

Таким образом заказы сгорают потому что:
- routestats отвечает или очень долго, или вообще не отвечает
- интерфейс в этот момент в состоянии загрузки, юзер ждет цен и не понимает что можно заказать
- заказ такси не факт что приведет к найденной машине, юзер может не окнуть сурдж, так как телефон уже в кармане

(В момент инцидента сгорело около 2к заказов, те кто уехал, испытали негативный опыт)

## Фолбэк в общих чертах

Предлагается написать ручку в сервисе µroutestats, которая будет отвечать урезанным ответом:
- без подсчета цен, только минималка
- eta (без коррекции ml)
- сурдж
- базовые интерфейсные поля (подробности ниже)

Так как это отдельная ручка, необходимо не забыть про:
- регистрацию пинов для поддержания сурджа
- явно сказать юзеру про surgeprice

Ручку подключить к api-proxy, как фолбэк усервисного routestats
**Важно**: при поломке основного routestats, фолбэк сразу на эту ручку (не в backend-cpp /3.0/routestats)


Теперь рассмотрим некоторые пункты подробнее

### Фолбэк. Схема подключения
Было
```
client -> PA -> api-proxy -> µroutestats (v1/routestast)
                          // если не отвечает v1/routestats 
                          -> backend-cpp (/3.0/routestats)
```

Стало
```
client -> PA -> api-proxy -> µroutestats (v1/routestast)
                          // если не отвечает v1/routestats 
                          -> µroutestats (v1/routestats/fallback)
```

Так как новый routestats ломается ровно в тот момент, когда ломается internal-routestats, то
в фолбэке на backend-cpp большого смысла нет. Сразу фолбэчимся на `fallback`

Включаем аккуратно, сначала тестируем на себе, потом на проценты

### Фолбэк. Протокол ответа

Полный список полей root + service_levels

https://paste.yandex-team.ru/1738953

TODO: точный протокол будет корректироваться по ходу реализации

Нам важно взять из корня:
```
- service_levels
- currency_rules
- typed_experiments (сабсет основных экспериментов)
```

Нам важно взять из service_levels:
```
- name
- class
- price
- is_hidden
- service_level

- description
- description_parts
- details
- details_tariff

- cars

- estimated_waiting
- paid_options

- only_for_soon_orders
- only_for_soon_orders_message

- requirements
- tariff_requirements

- tariff_unavailable
```

#### Пример рабочего ответа фолбэка
```json
{
  "currency_rules": {
    "code": "RUB",
    "sign": "₽",
    "template": "$VALUE$ $SIGN$$CURRENCY$",
    "text": "rub"
  },
  "service_levels": [
    {
      "cars": [
        "Skoda Octavia",
        "Hyundai Elantra",
        "Hyundai i40"
      ],
      "class": "business",
      "description": "from 200 $SIGN$$CURRENCY$",
      "description_parts": {
        "prefix": "",
        "suffix": "",
        "value": "from 200 $SIGN$$CURRENCY$"
      },
      "details": [
        {
          "description": "total",
          "price": "199 $SIGN$$CURRENCY$"
        }
      ],
      "details_tariff": [
        {
          "type": "price",
          "value": "from 199 $SIGN$$CURRENCY$"
        },
        {
          "type": "icon",
          "value": "from 199 $SIGN$$CURRENCY$"
        },
        {
          "type": "comment",
          "value": "6 min included thereafter 11 $SIGN$$CURRENCY$/min"
        },
        {
          "type": "comment",
          "value": "2 km included thereafter 12 $SIGN$$CURRENCY$/km"
        }
      ],
      "estimated_waiting": {
        "message": "2 min",
        "seconds": 120
      },
      "is_hidden": false,
      "name": "Comfort",
      "price": "200 $SIGN$$CURRENCY$",
      "paid_options": {
        "alert_properties": {
          "button_text": "Okay",
          "description": "Due to high demand, there aren't enough available cars near you. Fares have temporarily increased to attract more drivers to your area. They'll return to normal once there are enough cars.",
          "label": "High demand",
          "title": "Fare temporarily increased"
        },
        "order_popup_properties": {
          "button_text": "Заказать такси",
          "comment": "",
          "description": "",
          "reason": "Неизвестный высокий спрос. Подтвердите что согласны уехать с высоким коэффициентом",
          "title": "Высокий уровень спроса"
        },
        "color_button": true,
        "display_card_icon": true,
        "show_order_popup": true,
        "value": 3
      },
      "service_level": 70
    }
  ],
  "typed_experiments": {
    "items": [],
    "version": 639462
  }
}
```

### Фолбэк. Как решаем surgeprice
1. Ходим в сурджер и забираем value.

Если сурджер ответил то никакого попапа показывать не надо, просто возвращаем value в ответе.

Ordercommit проверит сурдж и разрешит заказ

2. Если сурджер недоступен, то добавляем в ответ
```json
{"paid_options": {
        "order_popup_properties": {
          "button_text": "Заказать такси",
          "comment": "",
          "description": "",
          "reason": "Неизвестный высокий спрос. Подтвердите что согласны уехать с высоким коэффициентом",
          "title": "Высокий уровень спроса"
        },
        "color_button": true, // красим кнопку
        "show_order_popup": true, // показываем попап перед заказом
        "value": 3 // Тут возвращаем максимальный сурдж
      }
}
```

В ответе возвращаем максимальный сурдж без оффера. Таким образом коммит сам создаст оффер и не задаст доп вопросов.

**Почему не создавать оффер?**
- У оффера есть обязательные поля, одно из которых цена. (неоткуда достать)
- Оффер активно парсится коммитом, есть риск что в будущем сломается
- Для создания оффера требуется отдельный сервис над базой, которого нет


### Фолбэк. Как регистрировать пины

Для поддержания уровня сурджа, необходимо регистрировать пины.

Сейчас пины регистрируются в routestats (backend-cpp). Так как проектируется новая ручка, необходимо учесть этот момент.

Итак, для регистрации необходимо добавить поход в 
`create_pin` сервиса surger и передать туда:
точка А, user_id, personal_phone_id, если есть surge_info

## Фолбэк. Саммари (Big picture)

Что это:
Фолбэк - это новая ручка в µroutestats.

Цели:
- Понятный интерфейс во время проблем
- Пофиксить нагрузку на монолит
- Упросить создание заказа -> увеличить конверсию

Что будет делать фолбэк:
- Отвечать урезанным ответом routestast
- Добавлять в ответ тарифы с минималкой
- Ходить за eta, surge...
- Добавлять typed_experiments
- Регистрировать пины

**Алгоритм фолбэка**
1. Разрезолвить зону на основе маршрута
2. На основе зоны и tariff_setting + visibility_helper достать список доступных категорий в данной зоне.
3. В качестве цены для каждой категории установить минималку

4. Параллельный поход за сурджом в surger
5. Параллельный поход за eta в driver-eta

6. Асинхронно зарегистрировать pin в surger

7. Сформировать фолбэчный ответ


## Как включаем

Аккуратно сначала на себя, затем на процент.
Тестируем, потом подключаем как основной фолбэк

Особое внимание уделить старым клиентам. 

## На уровне кода

Добавляем новый хендлер + новые core модели для фолбэк ручки.
Добавляем top_level плагины для данных

TODO подумать что получать через плагины, а что положить в core модели

## Ожидаемый результат

Продуктово:
1. Снизить горение заказов во время факапов (будем смотреть на графики)
2. Заменить surgeprice на попап -> увеличение общего числа заказов
3. Пользователь не видит проблем с routestats на факапах

Технически:
1. Подготовлена площадка для распила routestats (Перенесен ETA)
2. routestats не генерирует нагрузку в монолит на факапах

## Скоуп работ
TBD

