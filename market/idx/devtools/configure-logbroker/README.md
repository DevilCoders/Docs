## Описание
Тулза для создания топиков и читателей в LB.
Сделанна конкретно для создания топиков и читателей,
которые ипользуются при бысторй доставке данны их через SAAS HUB в RTY.

## Структура путей в LB
Топики и читатели для конкретного окружения и цвета находятся в:
/market-quick/{prod,testing}/{main,blue,red}/...

Читатели имею имена вида "reader-0", "reader-1"...
Каждый читатель соотвествует одноми миникластеру и читает из нескольких шардов.

Топики имеют вид "shard-0-0", "shard-1-1"... "shard-7-7"
Каждый топик соответствует одному шарду(паре шардов индекса)

Разделение оферов по цветам:
- main - все офера, включая красные и синие
- red - только красные офера
- blue - только синие офера

NB: Это актуально только на момент написания, офера распределяются по топикам в SAAS HUB тут: https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/quick/saashub/etc/conf/market-saas-hub.cfg

## Примеры
Создать топики для красного маркета в проде:
`./configure-logbroker --environment prod --color red -m MARKETINDEXER-25581 make_topics`

Создать 6 читателей для красного маркета в проде(топики уже должны быть созданны, что бы можно было read-rules создать)
`./configure-logbroker --environment prod --color red -m MARKETINDEXER-25581 make_readers --readers 6 --dc sas --dc man --dc vla`
Через `--dc` указываются ДЦ, куда доложно идти зеркалирование
https://wiki.yandex-team.ru/logbroker/docs/config/#read-rule

## TODO
Надо бы это переписать на gRPC API это лучше будет, чем вывод консольной тулзы парсить
https://wiki.yandex-team.ru/logbroker/docs/config/#api
