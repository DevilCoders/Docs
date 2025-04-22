Здесь будут лежать разные полезные yql-скрипты, которыми иногда нужно что-нибудь посчитать.

Как использовать:
1. Положить шаблон в эту директорию
2. Прописать в `marketindex/ya.make` ресурс в директиву `RESOURCE`
3. Подключить в `from library.python import resource`
4. Загрузить шаблон `yql_query_template = resource.find('/yql/calc-uc-age')` и подставить параметры через `yql_query_template.format(...)`
