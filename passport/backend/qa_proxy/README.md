## qa-proxy

https://passport-qa-proxy.yandex.net:8888

qa-proxy пересылает запросы в бекенды Паспорта, проверяя, что запрос поступает от доверенных `tvm_client_id`.

### Что делает прокси
1. Получает запрос
2. Смотрит на число одновременных запросов, и убеждается, что оно не превышает допустимое
3. Вынимает из запроса заголовок `Ya-Proxy-TVM-Ticket` и проверяет, что в нём содержится service-ticket от одного из разрешённых client_id
4. Получает из запроса заголовок `Ya-Proxy-Target-Url` и убеждается, что это один из разрешённых хостов
5. Если всё ок, отправляет запрос на целевой хост и пересылает ответ клиенту. Иначе не отправляем запрос и отвечаем клиенту ошибкой

### Дырки
Дырки от прокси до целевого хоста должны быть заказаны в [Панчере](https://puncher.yandex-team.ru/?create_ports=443&create_protocol=tcp&create_sources=_PASSPORT_QA_PROXY_NETS_&create_until=persistent)

### TVM
TVM `client_id` прокси `2027050`

### Сборка
`ya package ./deb/yandex-passport-qa-proxy.json`

### Выкладка
Выкладка происходит автоматически через [CI](https://a.yandex-team.ru/projects/passp/ci/releases/timeline?dir=passport%2Fgo%2Fdaemons%2Fqa_proxy&id=passport-qa-proxy-release) после вливания PR в `trunk`.

[Deploy stage](https://deploy.yandex-team.ru/stages/passport-qa-proxy-stable)

