## takeout tester

Простенькая говно-приложенька для проверки корректности валидации TVM тикетов у takeout ручек.

**Для корректной работы нужно иметь доступ в сервис для TVM client `2010664` (или любого своего)**

## example usage
```
$ ./takeout --url=https://testing.suburban-selling.rasp.common.yandex.net/gdpr_takeout --client-id=2002606 --uid=4012515154

----------
call test_normal:
{'status': 'ok', 'data': {'orders.json': '[...]'}}
----------


----------
call test_wrong_dst:
{'status': 'error', 'message': 'access forbidden'}
----------


----------
call test_wrong_src:
{'status': 'error', 'message': 'access forbidden'}
----------


----------
call test_wo_tvm:
{'status': 'error', 'message': 'access forbidden'}
----------


----------
call test_tvm_knife:
{'status': 'error', 'message': 'access forbidden'}
----------

```

Где:
   - `url` - урл целевой ручки
   - `client-id` - TVM client id целевого сервиса
   - `uid` - UID юзера по которому выгружаем данные
