# Masstransit dump
Скрипт для выгрузки статики из npro в PostgreSQL.  
Для запуска необходимо собрать бинарник:
```
cd arc/arcadia/maps/tools/geocontent/masstransit_dump/ && ya make -r
```
Затем после успешной сборки скопировать бинарь в хомяк:  
```
cp masstransit_dump ~/
```
И сделать:  

```
./masstransit_dump 
```

## Attention
Изначально скрипт будет падать примерно со следующей ошибкой:
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

Результатом выполнения бинарника, будет файл-  ***.gpkg**  
Который складывается сюда:  
**S:\Peutinger\Threads\data_//<дата_выгрузки>//**  
  
На выходе получается 3 слоя:  
**stops** - остановки  
**threads** - нитки  
**thread_stops** - связь ниток с остановками  

TODO:  
Реализовать интервалы хождения ТС.  
Время прибытия/отправления ТС от остановки.
