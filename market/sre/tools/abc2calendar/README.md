Инструмент для синхронизации дежурств из ABC в Календарь
=======================================================

### Получение секретов

Перед началом использования необходимо получить секреты. 

TVM секрет приложения, заведенного для синхранизации расписания и календарей можно найти тут: https://nda.ya.ru/t/aIjX01MC3VuKRD

```
export ABC2CAL_TVM_SECRET=...
```
Oauth токен для получению user-ticket-а от TVM можно найти тут: https://nda.ya.ru/t/wjXuN6JH5FUxHV
```
export ABC2CAL_OAUTH_TOKEN=...
```

### Как ипсользовать:
```
ya make -t && bin/abc2calendar
```
