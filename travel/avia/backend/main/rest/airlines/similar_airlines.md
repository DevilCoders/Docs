# Описание ручки
Ручка возвращает похожие авиакомпании, если похожих было меньше 6, то дополняет до 6 из топа по национальной версии.


## Формат запроса:
```
curl -X GET <API-HOST>/rest/airlines/similar_airlines/<national_version>/<lang>/<company_id>
```
*national_version* - нац. версия
*lang* - язык интерфейса пользователя
*company_id* - id авиакомпании

## Формат ответа:

```
/rest/airlines/similar_airlines/ru/ru/26
{
   "status": "ok",
   "data": [
      {
         "score": 0.4390863,
         "id": 23,
         "slug": "s7_s7-airlines",
         "title": "S7 Airlines",
         "logo": "https://avatars.mds.yandex.net/get-avia/233213/2a0000015a80532552c435919c4707269e8e/svg"
      },
      {
         "score": 0.3604061,
         "id": 30,
         "slug": "u6_ural-airlines",
         "title": "Уральские авиалинии",
         "logo": "https://avatars.mds.yandex.net/get-avia/200364/2a0000015a80534291a2010a3106b2bddd70/svg"
      },
      {
         "score": 0.27918783,
         "id": 29,
         "slug": "ut_utair",
         "title": "ЮТэйр",
         "logo": "https://avatars.mds.yandex.net/get-avia/365172/2a0000015a805343afbd5d771001eaf49294/svg"
      },
      {
         "score": 0.21827412,
         "id": 2543,
         "slug": "n4_nordwind-airlines",
         "title": "Nordwind Airlines",
         "logo": "https://avatars.mds.yandex.net/get-avia/365172/2a0000015a80531f51c470286145377522af/svg"
      },
      {
         "score": 0.19543147,
         "id": 9,
         "slug": "nn_vim",
         "title": "ВИМ-Авиа",
         "logo": "https://avatars.mds.yandex.net/get-avia/365172/2a0000015a80533a9ce1b06fca54cc4b7813/svg"
      },
      {
         "score": 0,
         "id": 2048,
         "slug": "ze_eastar-jet",
         "title": "Eastar Jet",
         "logo": ""
      }
   ]
}
```
Если АК не нашлась:
```
{
   "status": "ok",
   "data":[]
}
```