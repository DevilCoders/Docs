# Вопросы безопасности/сетевых и прочих доступах (IDM/Pucher/Cauth)
## Ручка для поиска макроса по IP {#puncher_search_ip_marcro}
https://puncher.yandex-team.ru/api/dynfw/parents?q=<fqdn/ip>


## Что делать, если IDM не работает, но нужно срочно выдать какие-то права пользователям (дежурным 2 линии)
1. Запросы нужно делать от робота, поэтому идем в секретницу и достаем токены YP для xdc [тут](https://yav.yandex-team.ru/secret/sec-01d4a3gjzb3mcwhb57e53691hj/explore/versions), для sas-test/man-pre [тут](https://yav.yandex-team.ru/secret/sec-01dq82qp866hcc1att3bvcad02/explore/versions).
2. Делаем запрос на добавление прав. В данном примере добавляем write на весь объект.
```
YP_TOKEN=<token> ya tool yp update <object_type> <object_id> --set /meta/acl/end '{action=allow;subjects=[<user>;];permissions=[write;];}' --address <cluster>
```
3. Потом нужно не забыть удалить выданные права и попросить пользователя запросить через IDM. **Будьте внимательны при удалении одного ace (AccessControlEntry), командой --remove /meta/acl можно снести весь список прав.**
```
ya tool yp get <object_type> <object_id> --address <cluster> ** находим индекс нужного ace в списке acl **  
YP_TOKEN=<token> ya tool yp update <object_type> <object_id> --remove /meta/acl/<index> --address <cluster>
```
