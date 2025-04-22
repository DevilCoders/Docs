# Интеграционные тесты для демона FASTRES2

## Суть теста:
1. поднимается демон поверх фиксированной базы данных (ресурсы вида "db.*" в ya.make);
2. с помощью инструмента [servant_client](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/tools/servant_client) в демона посылается запрос (ресурсы вида "request.*\.json" в ya.make);
3. ответ демона сравнивается с эталоном.

## Как подложить базу данных:
Можно воспользоваться инструментом [fastres2pycl](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/wizards/fastres2/fastres2pycl):
```
./fastres2pycl --mongo-uri <MONGO_URI> -mongo-db <MONGO_DB> --mongo-collection <MONGO_COLLECTION> dump-db --file <DB_FILE>
ya upload --ttl inf <DB_FILE>
```
Удобно, что можно дампить любую коллекцию, в частности ту, которая использовалась в процессе разработки и отладки.

## Как подложить запрос:
1. Делаем поисковой запрос с ```dump_source_request=FASTRES2```;
2. Идем в SeTrace, ищем там eventlog Аппхоста (сейчас интересует источник WEB1);
3. Ищем запрос в FASTRES2, копируем его ([тут более наглядная инструкция](https://jing.yandex-team.ru/files/zhevnerchuk/Data.f5c57ab.png));
4. Заливаем в Sandbox. **Важно:** servant_client понимает файлы, в которых каждый запрос -- это отдельная строчка, то есть нужно записать весь json запроса на одну строку, а не дампить json в файл.
