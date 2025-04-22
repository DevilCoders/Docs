## TVM

Александрия использует TVM для аутентификации в сервисах Blackbox и invapi Racktables.

Для проверки tvm аутентификации нужно:

1) Установить [tvmtool](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#izpypi):

2) Сделать [конфиг для tvmtool](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#konfig) alexandria_tvm.json,  

секреты можно посмотреть тут:  
https://yav.yandex-team.ru/secret/sec-01esr9a63r6ncjcfxz4n35grs4/explore/versions  
https://yav.yandex-team.ru/secret/sec-01esr5rdxan6jdf7e03132caaw/explore/versions  
https://yav.yandex-team.ru/secret/sec-01esr5qy1sqv4j51f600f9pf17/explore/versions  


```json
{
    "BbEnvType": 2,
    "clients": {
        "alexandria": {
            "secret": "SECRET",
            "self_tvm_id": 2025424,
            "dsts": {
                "blackbox": {
                    "dst_id": 223
                },
                "racktables": {
                    "dst_id": 2020198
                }
            }
        }
    }
}
```
(2025424: alexandria dev)

3) `TVMTOOL_LOCAL_AUTHTOKEN=00000000000000000000000000000000 tvmtool -c alexandria_tvm.json --port 13948`

### Пояснение к версии с Invapi
Конфигурационный файл для запуска Александрии даёт возможность указать два взаимоисключающих ключа: tvmtool и tvmapi.  
Для запуска в стейджинге и на локальной машине предполагается использовать TVMTOOL.
Для запуска на noc`ах подходит TVMAPI.

### Как ключи попадают на сервера RT и стейджинг
Через salt
https://a.yandex-team.ru/arc_vcs/admins/salt-media/noc/roots/units/racktables/files/tvmtool.conf 
https://a.yandex-team.ru/arc_vcs/admins/salt-media/noc/roots/nocdev-staging.sls 

## Схема
![процесс авторизации](alexandria_auth_v05.png "alexandria auth" =660x460)