# Elama Backoffice Frontend


Для запуска локального TVMtool 
tvmtool --port 8001 --auth tvmtool-development-access-token

Для создания сертификатов:
1. Заходим в папку server в терминале: cd ./server
2. Выполняем команды:
openssl genrsa -out server.key 2048
openssl rsa -in server.key -out server.key
openssl req -sha256 -new -key server.key -out server.csr -subj '/CN=local.yandex-team.ru'
openssl x509 -req -sha256 -days 365 -in server.csr -signkey server.key -out server.crt
3. Если браузер "ругается" на сертификат, то выполняем действия [по ссылке](https://wiki.yandex-team.ru/sigorilla/crt-hsts/)

Получить TVM_SECRET можно [тут](https://abc.yandex-team.ru/services/elama_back_office/resources/?view=consuming&layout=table&supplier=14&type=47&show-resource=41605800)
