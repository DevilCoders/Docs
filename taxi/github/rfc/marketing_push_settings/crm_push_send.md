### Изменения для бэкенд фильтрации
На данный момент все пуши от crm приходят с intent "crm":
https://yql.yandex-team.ru/Operations/X41ee5dg8rzeGB_zRKIF7ObYNx2FWTLCK4gX7cuWkj8=

Обсудили с https://staff.yandex-team.ru/v-belikov типизацию рассылок по полю intent, где каждый тип маркетинговой рассылки будет 
маппиться в нужный тип фильтра по конфигам на стороне ucommunications

### На стороне ucommunications
1) Преобразовать intent -> marketing_type, использовать в xiva 
2) Добавить marketing_type в payload пуша
```json5
{
    "payload": {
          "tags": ["drive_news"], // массив на случай использования нескольких тэгов, в mvp планируем отправлять пуши с 1 тэгом
    
          "id": "f0ccc92cb0b3e0de6d4ef796cc8be9d4",
          "msg": "Если б мишки были пчелами",
          "deeplink": "",
          "extra": {
            "save_promocode": true
          }
        }
}
```
