[Документация по офлайн метрике почтового поиска](https://wiki.yandex-team.ru/Pochta/analytics/offline-mail-search/)

## Когда использовать

Если при редеплое сбросился эфемерный диск.

## Как использовать

Скачать из секретницы все нужные секреты.

https://yav.yandex-team.ru/secret/sec-01dhadjjz7vasxy1ketwrst8wx

Проверить поля accounts.json или другого конфига. url - адрес скрепера, 
на котором создавать аккаунты

Запустить `start.py -c accounts.json`

## Описание аккаунта:

```json
{
      "system": "google",
      "name": "basket25",
      "secrets": [
        {
          "name": "StoredCredential",
          "path": "secrets/StoredCredential25"
        },
        {
          "name": "credentials",
          "path": "secrets/gcredentials.json"
        }
      ],
      "properties": {
        "hostUrl": "https://mail.google.com"
      }
    }
```

system - система, в которой будет создан аккаунт

name - имя нового аккаунта

properties - параметры аккаунта, пока только url системы. 

secrets - список секретов, нужных для создания аккаунта 
(см Необходимые секреты в вики).

https://wiki.yandex-team.ru/Pochta/analytics/offline-mail-search/mail-scraper-for-user/#m-upravlenieakkauntami

## Описание секрета
```json
{
  "name": "credentials",
  "path": "secrets/gcredentials.json"
}
```
name -  имя секрета (credentialPart)

path - расположение файла с секретом. В accounts.json все секреты 
складываются в директорию secrets.