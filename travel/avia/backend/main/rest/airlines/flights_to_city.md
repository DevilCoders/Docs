# Описание ручки
Ручка возвращает до 6 самых популярных авиакомпаний для города по сумме кликов на неё в переданный город по переданной национальной версии.


## Формат запроса:
```
curl -X GET <API-HOST>/rest/airlines/flights_to_city/<settlement_id>
```

## URL Params

Required:
national_version=[string] - нац. версия # example: national_version=ru
lang=[string] - язык интерфейса пользователя # example: lang=de

## Success Response:

```
/rest/airlines/flights_to_city/2?national_version=ru&lang=ru
{
  "status":"ok",
  "data":[
    {
      "logo":"https:\/\/avatars.mds.yandex.net\/get-avia\/233213\/2a0000015a80533f813c037de08cb5fd7f8f\/svg",
      "title":"Россия (FV)",
      "score":47217,
      "id":8565,
      "slug":"su_rossia"
    },
    {
      "logo":"https:\/\/avatars.mds.yandex.net\/get-avia\/233213\/2a0000015a80532552c435919c4707269e8e\/svg",
      "title":"S7 Airlines (S7)",
      "score":41181,
      "id":23,
      "slug":"s7_s7-airlines"
    },
    {
      "logo":"https:\/\/avatars.mds.yandex.net\/get-avia\/365172\/2a0000015a805343afbd5d771001eaf49294\/svg",
      "title":"ЮТэйр (UT)",
      "score":29648,
      "id":29,
      "slug":"ut_utair"
    },
    {
      "logo":"https:\/\/avatars.mds.yandex.net\/get-avia\/200364\/2a0000015a80534291a2010a3106b2bddd70\/svg",
      "title":"Уральские авиалинии (U6)",
      "score":26321,
      "id":30,
      "slug":"u6_ural-airlines"
    },
    {
      "logo":"https:\/\/avatars.mds.yandex.net\/get-avia\/365172\/2a0000015a80533f482fe78d9b42e51f22d4\/svg",
      "title":"Победа (DP)",
      "score":24345,
      "id":9144,
      "slug":"dp_pobeda"
    },
    {
      "logo":"https:\/\/avatars.mds.yandex.net\/get-avia\/365172\/2a0000015a80533a9ce1b06fca54cc4b7813\/svg",
      "title":"ВИМ-Авиа (NN)",
      "score":13168,
      "id":9,
      "slug":"nn_vim"
    }
  ]
}
```