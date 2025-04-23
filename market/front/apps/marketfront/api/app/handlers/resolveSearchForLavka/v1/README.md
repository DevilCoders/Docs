# Резолвер
resolveSearchForLavka

Конфигурация для интеграции Маркета в Лавку.
Возвращает список маркетных товаров в формате, принимаемом лавкой,
а также ссылки:
- на полную маркетную выдачу
- для рекламного маректного баннера, отображаемого в лавке


## Пример запроса

```

curl --request POST \
  --url 'https://<FAPI_HOST>/api/v1?name=resolveSearchForLavka' \
  --header 'api-platform: ANDROID' \
  --header 'content-type: application/json' \
  --header 'cookie: x-yandex-icookie=123' \
  --header 'x-user-authorization: OAuth <your token>' \
  --cookie x-yandex-icookie=123 \
  --data '{"params": [{
	"gps": "37.587093,55.733974",
	"text": "телефон",
	"count": 1
}]}'
```

## Пример ответа

https://paste.yandex-team.ru/8909903/html
