# Панорамные тропы 
Стенд для разметки панорам.  
Для запуска необходимо собрать бинарник:
```
cd arc/arcadia/maps/tools/geocontent/pano_roads/ && ya make -r
```
Затем после успешной сборки сделать:  

```
./panorama_makers --port <PORT>
```

## Attention
Изначально сервер будет падать примерно со следующей ошибкой:
```
library.python.vault_client.errors.ClientError: {'request_id': '6432c3c156127cefa75c10b270adf766', 'api_request_id': '6432c3c156127cefa75c10b270adf766', 'blackbox_error': 'expired_token', 'code': 'invalid_oauth_token_error', 'environment': 'production', 'hostname': 'vault-s2.passport.yandex.net', 'message': 'Invalid oauth token', 'status': 'error'}
```

Для успешного подключения к `yav` по ssh из dev-тачки следует выполнить следующее:

[Найти в документации про OAuth token](https://vault-api.passport.yandex.net/docs/)


```
export YAV_TOKEN='<TOKEN>'
```

Затем скрипт может ругнуться на отсутвие SSL сертификата к PostgreSql базе:

```
psycopg2.OperationalError: root certificate file "/home/yasen/.postgresql/root.crt" does not exist
```
Решение:
```
mkdir ~/.postgresql && \
wget "https://crls.yandex.net/allCAs.pem" -O ~/.postgresql/root.crt && \
chmod 0600 ~/.postgresql/root.crt
```
[Подробно в документации](https://docs.yandex-team.ru/cloud/managed-postgresql/operations/connect#configuring-an-ssl-certificate)

Результатом выполнения бинарника, будет запущен flask сервер.  
Который будет доступен на запущенной dev тачке:  **hostname:port**  
  
Разметка дорожного графа для последующего проезда панорамамобиля является:  
**Выгрузка** - сборка из [ymapsdf](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest "latest") дорожного графа в PostgreSQL  
**Разметка** - проставление аттрибутов дорожному графу:
* ##### kategor 1 - 15 метров (кнопка 1) 
* ##### kategor 2 - 30 метров (кнопка 2) 
* ##### kategor 3 - пешеходка (кнопка 3)
* ##### kategor 4 - 5 метров  (кнопка 4) 
* ##### kategor 5 - 50 метров (кнопка 5) 
* ##### kategor 0 - удаление  (кнопка 0) 
 
**Сохранение** - скачивание результатов с сервера  
* ##### Сохранение всего графа 
* ##### Сохранение размеченного 

### TODO: 
* Выгружать шлагбаумы  
* Разметка из файла
* Отсечь дороги без доступности авто в дизайне (тонкая линия)
* Оверзум треков

