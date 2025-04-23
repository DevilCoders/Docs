1. получить токен
```bash
ya tool tvmknife get_service_ticket sshkey -s 2030045 -d 2030045 
```
2. создать файл http-client.private.env.json формата:
```json
{
  "prod": {
    "token": "ТОКЕН"
  }
} 
```

