# Описание ручки
Ручка возвращает список всех валют и их локализации

## Формат запроса:
```
'/rest/currencies/<national_version>/<lang>'
```
*national_version* - национальная версия
*lang* - язык интерфейса пользователя

## Формат ответа:

```
https://<host>/rest/currencies/ru/ru
{
  "status": "ok",
  "data": [
        {
            "title_in": "в тур. лирах",
            "code": "TRY",
            "template_cents": "0.%d&nbsp;<unit>TL</unit>",
            "template": "%d.%02d&nbsp;<unit>TL</unit>",
            "title": "турецкие лиры",
            "template_whole": "%d&nbsp;<unit>TL</unit>",
            "iso_code": "TRY",
            "id": 7
        },
        {
            "title_in": "",
            "code": "TRY",
            "template_cents": "",
            "template": "",
            "title": "",
            "template_whole": "",
            "iso_code": "TRY",
            "id": 7
        }
        ...
  ]
}
```


## Особенности:
Список валют кэшируется до рестарта сервиса (то есть на сутки).

Если локализации для валюты нет, то переводы будут равны пустым строкам.

Почти по всему коду мы используем `code`, но все наши партнеры уже переползли на  `iso_code`
