# Креатив

По сути, креатив - это ассет баннера. Как логотип или кнопка. Но он гораздо сложнее. Для креативов есть отдельное приложение [canvas](https://deploy.yandex-team.ru/stages/direct-canvas-production/status/canvas/) и отдельная [база данных](https://yc.yandex-team.ru/folders/fooa07bcrr7souccreru/managed-mongodb/cluster/aef189d8-93bf-4bca-a416-cf2c09bd9758?section=overview).

## Виды

Canvas (канва, холст с англ.) - интерфейс, для создания креативов, он же конструктор креативов.

Конструктор, состоит из частей:
1. Canvas - первый html конструктор в котором можно создать себе креатив в веб-редакторе из готового шаблона
2. html5 - Конструктор для html5 креативов, в который можно либо залить *.zip с креативом, либо картинку, которую конструктор сам обернет в креатив
3. video - Видео конструктор для создания видео по шаблону или заливки файлом (/video/files)

## Релизы canvas
[Документация как собрать релиз](https://docs.yandex-team.ru/direct-dev/guide/releases/canvas)


## Мониторинги
[основной дашборд](https://grafana.yandex-team.ru/d/AQ9gPJPWz/canvas-direct?orgId=1&refresh=5m)  
[ошибки](https://juggler.yandex-team.ru/check_details/?host=direct.prod_apps-health&service=canvas&last=1DAY)  
[Логи ошибок бэк](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'span_id~'class_name~'message)~conditions~(service~'direct.canvas~log_level~'ERROR)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)  
[Логи фронт](https://direct.yandex.ru/logviewer#~(logType~'nginx_access~form~(fields~(~'log_time~'remote_addr~'vhost~'method~'req_uri~'status~'time~'upstream_time~'resp_size~'upstream_reqid~'hostname)~conditions~(status~'*3e*3d500~vhost~'canvas-back.direct.yandex.net)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)

## С кем интеграция
- ротор
- intapi
- rtbhost
- stillage
- Конструктора Турболендингов
- scrapper

## Разработка
[Локальный запуск с базой devtest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/canvas/docs/runlocal-devtest.md)

запуск на бете Канваса [DIRECTKNOL-32](https://st.yandex-team.ru/DIRECTKNOL-32)

## База данных
Сами бинарики храняться в mds. Метаинформация хранится в монге. И в таблице [perf_creatives](https://direct-dev.yandex-team.ru/db/ppc/tables/perf_creatives.html) MySQL. Отправляется в RTBHost, у них есть [выгрузка на HAHN](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/yabs/dict/DSPCreative)

Подключаться с клиента `mongo --ipv6 $MONGODB_CONNECTION_STRING`
строку подключения можно брать из секретницы
[Тестовые секреты](https://yav.yandex-team.ru/secret/sec-01d4qht9ftyb3qxpa507jbng5g/explore/versions)  
[Прод только чтение](https://yav.yandex-team.ru/secret/sec-01d88mwm93ym5maymtnfrn42kh/explore/versions)  

список коллекций `show collections`

пример запроса `db.html5_batches.find({'product_type':'CPM_YNDX_FRONTPAGE',name:'десктоп'}).limit(5).pretty()`


## Библиотечные элементы
[картинки](https://a.yandex-team.ru/arc/trunk/arcadia/direct/canvas/src/main/resources/stock/files.json)  
категории гугловые на 2016 год [https://a.yandex-team.ru/arc/trunk/arcadia/direct/canvas/src/main/resources/stock/categories.json](https://a.yandex-team.ru/arc/trunk/arcadia/direct/canvas/src/main/resources/stock/categories.json)
