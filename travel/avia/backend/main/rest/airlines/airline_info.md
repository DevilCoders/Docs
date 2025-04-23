# Описание ручки
Ручка возвращает информацию о базовом тарифе и рейтинге АК, если есть больше 5 рейсов.



## Формат запроса:
```
curl -X GET <API-HOST>/rest/airlines/airline_info/<company_id>
Если не указать company_id - вернет все авиакомпании
curl -X GET <API-HOST>/rest/airlines/airline_info
```
*company_id* - id авиакомпании

Дополнительные параметры:
- *lang* - язык
- *fields* - указание полей для получения. Поля передаются список через запятую, например "?fields=id,title". Если поле не передано, возвращаются все поля.
Можно запрашивать поля:
```
id, alliance, title, url, logoSvg, color, slug, iata, sirena, icao, rating, default_tariff, seo_description_i18n_key, baggage_rules, baggage_rules_url, registration_url,
baggage_length, baggage_width, baggage_height, baggage_dimensions_sum,
carryon_length, carryon_width, carryon_height, carryon_dimensions_sum,
```
## Формат ответа:

```
/rest/airlines/airline_info/26
{
   "status": "ok",
   "data": {
      "rating": {
         "delayed3060": 3,
         "flightCount": 7,
         "delayedMore90": 0,
         "canceled": 2,
         "goodCount": 64,
         "scores": 1078,
         "delayed6090": 9,
         "delayedLess30": 9,
         "avgScore": 8.764228,
         "badPercent": 47,
         "outrunning": 21,
         "badCount": 59
      },
      "default_tariff": {
         "carryon": true,
         "baggage_pieces": 1,
         "baggage_allowed": false,
         "description": "По умолчанию",
         "carryon_norm": 8,
         "mask": "",
         "published": true,
         "baggage_norm": 23,
         "id": 83,
         "avia_company": 2
      }
      "seo_description_i18n_key": "https:\/\/tanker.yandex-team.ru\/?project=Avia&keyset=company_seo_description&branch=master&key=26_su_aeroflot",
      "registration_url": "http:\/\/www.aeroflot.com\/cms\/online_registration",
      "baggage_rules": "В салон можно взять ручную кладь: сумку, рюкзак или небольшой чемодан. Ограничения по размеру и весу ручной клади можно посмотреть на сайте авиакомпании. Кроме того, в правилах авиакомпании перечислены предметы, которые тоже могут лететь в салоне. Это дамская сумочка или мужской портфель, папка для бумаг, зонтик, трость, букет цветов, верхняя одежда, портативный компьютер, фотоаппарат, видеокамера, печатные издания для чтения в полёте, детское питание на время полёта, детская люлька при перевозе ребёнка, костюм в портпледе, мобильный телефон, костыли, сумка с покупками из магазина duty free.\r\nПеред вылетом обязательно сверьтесь с правилами авиакомпании на её сайте — особенно если у вас с собой много разных вещей.",
      "baggage_rules_url": "http:\/\/www.aeroflot.ru\/ru-ru\/information\/preparation\/baggage"
      ...
   }
}
```

Запрос фильтров полей и языком: /rest/airlines/airline_info/26?lang=en&fields=id,title,url
```
{
    "status": "ok",
    "data": {
        "url": "http:\/\/www.aeroflot.ru\/",
        "id": 26,
        "title": "Aeroflot"
    }
}
```

```
Запрос фильтров полей и языком для всех АК: /rest/airlines/airline_info?lang=ru&fields=title
{
    "status": "ok",
    "data": {
        "2048": {
            "title": "Eastar Jet"
        },
        "2045": {
            "title":"Edelweiss Air"
        }
        ...
    }
}
```


Если АК не нашлась или для неё нет данных в базе, возвращаем null-ы
```
{
   "status": "ok",
   "data": {
      "rating": null,
      "default_tariff": null,
      "seo_description_i18n_key": null,
      "registration_url": null,
      "baggage_rules": null,
      "baggage_rules_url": null
   }
}
```
