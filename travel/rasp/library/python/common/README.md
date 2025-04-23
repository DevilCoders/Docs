common
===========

Common models and code for RASP family of services

Here belong:
- mysql_switcher (including connectdb)
- stripped models
- distributed cache methods
- common global settings (local settings should be handled by yandex-rasp-common package)
- ... (to be continued)
- initially specific modules (form parser/search/station schedule) will be here


## Как выгружать секреты в qloud

Нужно, чтобы все секреты в common вытаскивались при старте, т.е. были в settings или configuration.
 Так мы заметим отсутствие секретов в выгрузке еще при запуске окружения.
 И сможем во время откатить.

Для продакшена, по дефолту мы берем значения из тестинга, поэтому его нужно тоже выгрузить. 

``rasp-vault qloud-export -t 'rasp-common and (production or testing)'``

``rasp-vault qloud-export -t 'rasp-common and testing'``

С полученым base64 создаем секреты в qloud типа, binary-base64,

Имя секрета ``vault-rasp-common-production-2018-08-17``, дата момента выгрузки, выгружать в файл.
``/etc/yav-secrets/rasp-common-production.json.gz``

Доступ нужно дать на весь проект ``rasp``.

Для тестинга аналогично.

Проверить, что секрет есть во всех окружениях:
```bash
rasp-vault need-secret --token='<token>' rasp vault-rasp-common-production-2018-08-17 | grep -E 'testing|prestable|production'
```
подробнее в https://github.yandex-team.ru/rasp/yandex-rasp-vault
