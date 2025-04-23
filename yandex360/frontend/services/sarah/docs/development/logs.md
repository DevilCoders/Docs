# Логи

Логи Duffman-а пишутся в папку `/app/log`  
Логи nginx пишутся в папку `/var/log/nginx`

Далее логи поставляются в LogBroker пользователю [sarah](https://lb.yandex-team.ru/logbroker/accounts/sarah)  
Поставляется 3 файла логов:  

| Топик в LB                 | Соответствующий файл логов     |
| -------------------------- |------------------------------- |
| `sarah/duffman-access-log` | `/app/log/duffman-access.tskv` |
| `sarah/duffman-http-log`   | `/app/log/duffman-http.tskv`   |
| `sarah/nginx-access-log`   | `/var/log/nginx/sarah.tskv`    |

Также поставляются логи awacs L7 балансера в топик [sarah/awacs-slb/sarah-awacs-slb-access-log](https://lb.yandex-team.ru/logbroker/accounts/sarah/awacs-slb/sarah-awacs-slb-access-log)

### YT

Из LogBroker-а логи отгружаются в YT в кластер Hahn в следующие таблички:  
- `sarah-duffman-access-log`
- `sarah-duffman-http-log`
- `sarah-nginx-access-log`
- `sarah-awacs-slb-access-log`

Актуальные права на чтение табличек:  
[sarah-duffman-access-log ACL](https://yt.yandex-team.ru/hahn/navigation?navmode=acl&path=//logs/sarah-duffman-access-log)  
[sarah-duffman-http-log ACL](https://yt.yandex-team.ru/hahn/navigation?navmode=acl&path=//logs/sarah-duffman-http-log)  
[sarah-nginx-access-log ACL](https://yt.yandex-team.ru/hahn/navigation?navmode=acl&path=//logs/sarah-nginx-access-log)  
[sarah-awacs-slb-access-log ACL](https://yt.yandex-team.ru/hahn/navigation?navmode=acl&path=//logs/sarah-awacs-slb-access-log)  

Права на чтение таблиц даны [ABC-группе](https://abc.yandex-team.ru/services/sarah/).  
Добавлять новых пользователей для чтения могут пользователи с ролью `Read approver`.  
Чтобы самому стать `Read approver`-ом, можно в интерфейсе запросить права через кнопку `Manage ACL`.
