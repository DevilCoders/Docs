## yt-perelivka-form

Батч джоба для перекладывания баз из карты сервисов в табличку в YT для интеграции с формами (forms.yandex-team.ru)

Запускается как батч джоба в Шиве

### Собрать protobuf
```make proto```

### Собрать образ
```
docker build -t registry.yandex.net/vertis/yt-perelivka-form:<version> .
docker push registry.yandex.net/vertis/yt-perelivka-form:<version>
```

(Сервис максимально простой, если надо будет его менять несколько раз - то надо настроить сборку в тимсити)

### Параметры:
- **SHIVA_ENDPOINT**
  
  Адрес АПИ Шивы


- **SHIVA_OAUTH_TOKEN**

  Токен для АПИ Шивы


- **YQL_TOKEN**

  Токен для YQL


- **YT_TABLE**

  Таблица, куда складывать список

  