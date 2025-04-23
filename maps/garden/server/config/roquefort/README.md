Скрипт gen_roquefort_config.py позволяет автоматически получить список ручек Огорода из кода и сгенерить конфиг для roquefort.

Команда для перегенерации конфига:
$ ya make -r && ./gen_roquefort_config


После перегенерации конфига необходимо поправить регулярки:
Регулярку:
"request_url": "/build/[^/]+"

исправить на:
"request_url": "/build/[^/]+/"


А так же вот это:
"request_url": "/contours/[^/]+/"

исправить на:
"request_url": "/contours/[^/]+"
