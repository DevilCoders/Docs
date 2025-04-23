Example - navigate url with empty cookie:
```
curl -i -X  POST http://localhost:8000/api/navigate   -H "Accept: application/json" -H "Content-Type: application/json"  -H "X-Auth-Token: secret"  -d '{ "url": "https://yandex.ru"}'
```

Example - navigate url with cookie:
```
curl -i -X  POST http://localhost:8000/api/navigate   -H "Accept: application/json" -H "Content-Type: application/json"  -H "X-Auth-Token: secret"  -d '{ "url": "https://yandex.ru", "cookies": [{"name":"asdasdasdasdasd","value":"bbbbbbbbbbbbbbb","url":"https://yandex.ru","domain":"yandex.ru","expires":1524584361}] }'
```