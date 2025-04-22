# Утилита prepare_partition для создания конфига разбиения рекламного фида на части

Утилита читает указанные файлы частей фида, вычисляет сколько офферов находятся в фиде для каждой категории. Далее категории сортуруются по размеру (по убыванию).
Максимальный размер части фида (в офферах) задан параметром ```-s```.
Проходим по отсортированному списку категорий. Категории, которые превышают максимальный размер фида попадают каждая в отдельные части фида.
Соседние в списке категории, не превышающие в сумме максимальный размер фида попадают в одну часть.

Можно подать файл ```-g``` с групировкой категорий, по какому-то признаку, это позволит сделать разбиение по депртаментам или кат. стримам

Созданный конфиг необходимо закоммитить в репозиторий (https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/pylibrary/mindexer_core/banner/banner_configs/configs/configs).

Он будет вкомпилирован в mindexer_clt, доставлен на мастера индексации и впоследствии будет использован при генерации фидов.

# Создания конфига
Максимальный размер части задаётся параметром ```-s```. Баннерокрутилосные системы прочитают лишь первые 100000 офферов из файла фида.
Необходимо учесть возможный рост количества офферов в категории. Поэтому логично задать параметр заметно < 100000, например 70000 офферов.

Через параметр ```-i``` необходимо перечислить url-ы на mds всеx частей фида.

Через параметр ```-f``` (обязательный) название поля, по которому будет разбиваться фид (например: id категории товара). Параметр не анализируется, просто пишется в выходной файл.

Выходной файл конфига (```-o```) содержит json с маппингои ```category_id->part_id``` (нумерация частей с 0, чтобы изменить используйте ```-n N```).

Параметр ```-n``` задает номер первой части (part_id) в мапинге выходного файла (применяется при пакетной обработки)

Параметр ```-d``` включает вывод статистической/отладочной информации в выходной файл (применяется для отладки и  дальнейшего анализа)

Параметр ```-g``` задает файл который описывает разбиение категорий на группы (департаменты / категорийные стримы).  категория(int)->группа(int/string)

## Пример создания конфига для фида k50-base-blue-bulky-all.json, состоящего из одной части:
```
~/arcadia/market/idx/export/awaps/prepare_partition/bin $ ./prepare-partition -s 70000 -f category_id -o k50-base-blue-not_bulky-all.json -i  https://market-idx-pub.s3.mds.yandex.net/k50-base-blue-not_bulky-all-1-part1.xml
2020-03-03 13:51:48,992 [DEBUG] Downloading https://market-idx-pub.s3.mds.yandex.net/k50-base-blue-not_bulky-all-1-part1.xml.
2020-03-03 13:51:50,616 [DEBUG] Parsing.
2020-03-03 13:51:55,804 [DEBUG] Searching for categories.
2020-03-03 13:51:56,290 [INFO] Found 1827 categories.
2020-03-03 13:51:56,668 [INFO] Partitioning categories into parts. Max number of offers in a part 70000
2020-03-03 13:51:56,674 [DEBUG] Stats:
2020-03-03 13:51:56,674 [DEBUG] parts    5         
2020-03-03 13:51:56,674 [DEBUG] offers   289265    
2020-03-03 13:51:56,674 [DEBUG] categories 1827      
2020-03-03 13:51:56,674 [INFO] Config written to k50-base-blue-not_bulky-all.json
```

## Пример создания конфига для фида k50-base-blue-not_bulky-all.json, состоящего из нескольких частей:
```
~/arcadia/market/idx/export/awaps/prepare_partition/bin $ ./prepare-partition -s 70000 -f category_id -o k50-base-blue-not_bulky-all.json -i \
https://market-idx-pub.s3.mds.yandex.net/k50-base-blue-not_bulky-all-5-part1.xml \
https://market-idx-pub.s3.mds.yandex.net/k50-base-blue-not_bulky-all-5-part2.xml \
https://market-idx-pub.s3.mds.yandex.net/k50-base-blue-not_bulky-all-5-part3.xml \
https://market-idx-pub.s3.mds.yandex.net/k50-base-blue-not_bulky-all-5-part4.xml \
https://market-idx-pub.s3.mds.yandex.net/k50-base-blue-not_bulky-all-5-part5.xml 
2020-06-11 12:39:58,803 [DEBUG] Downloading https://market-idx-pub.s3.mds.yandex.net/k50-base-blue-not_bulky-all-5-part1.xml.
2020-06-11 12:39:59,481 [DEBUG] Parsing.
2020-06-11 12:40:01,012 [DEBUG] Searching for categories.
2020-06-11 12:40:01,158 [INFO] Found 17 categories.
2020-06-11 12:40:01,262 [DEBUG] Downloading https://market-idx-pub.s3.mds.yandex.net/k50-base-blue-not_bulky-all-5-part2.xml.
2020-06-11 12:40:01,815 [DEBUG] Parsing.
2020-06-11 12:40:03,330 [DEBUG] Searching for categories.
2020-06-11 12:40:03,460 [INFO] Found 68 categories.
2020-06-11 12:40:03,550 [DEBUG] Downloading https://market-idx-pub.s3.mds.yandex.net/k50-base-blue-not_bulky-all-5-part3.xml.
2020-06-11 12:40:04,103 [DEBUG] Parsing.
2020-06-11 12:40:05,534 [DEBUG] Searching for categories.
2020-06-11 12:40:05,665 [INFO] Found 199 categories.
2020-06-11 12:40:05,755 [DEBUG] Downloading https://market-idx-pub.s3.mds.yandex.net/k50-base-blue-not_bulky-all-5-part4.xml.
2020-06-11 12:40:06,461 [DEBUG] Parsing.
2020-06-11 12:40:08,385 [DEBUG] Searching for categories.
2020-06-11 12:40:08,580 [INFO] Found 732 categories.
2020-06-11 12:40:08,720 [DEBUG] Downloading https://market-idx-pub.s3.mds.yandex.net/k50-base-blue-not_bulky-all-5-part5.xml.
2020-06-11 12:40:08,948 [DEBUG] Parsing.
2020-06-11 12:40:09,203 [DEBUG] Searching for categories.
2020-06-11 12:40:09,229 [INFO] Found 947 categories.
2020-06-11 12:40:09,249 [INFO] Partitioning categories into parts. Max number of offers in a part 70000
2020-06-11 12:40:09,255 [DEBUG] Stats:
2020-06-11 12:40:09,255 [DEBUG] parts    6         
2020-06-11 12:40:09,255 [DEBUG] offers   409538    
2020-06-11 12:40:09,255 [DEBUG] categories 1963      
2020-06-11 12:40:09,255 [INFO] Config written to k50-base-blue-not_bulky-all.json
```

## Пример использования для создания конфига для фида k50-beru-beru_offers-full.json (beru_offers_divided_without_separate)
, для разбиения по кат.стримам (и прочим группам), с листовыми категориями в одной части. На основе старого набора фидов котрые как-то побиты:

* Готовим файл и описанием разбиениея каегорий на кат.стримы. вида (ид_категория -> группа)
```
{"hyper_id":90408, "category_stream_name":"CEHAC"}
{"hyper_id":90417, "category_stream_name":"CEHAC"}
{"hyper_id":90418, "category_stream_name":"Auto and Machinery"}
{"hyper_id":90428, "category_stream_name":"Auto and Machinery"}
```

* prepare-partition На выхоте получим конфиг c разбиением на группы. В логе будут указаны категори которые больше лимита (запомнить их)
* Добавляем части для пустых группы, (? если надо) Подкладываем конфиг для регионов feeds_smart_config-region-template.json.
* Проверям, что все корректно. секцию "debug_info" можно удалить. Используется для контроля и отладки
* Для категорий которые не входят в один файл, задаем руками неободимое количество частей (в "part_oversizes")
* Проверяем что в "split_field_name": <field>, указано корректное поле.
* На готовом, новом конфиге, запустить genarate_category_to_part.py  https://a.yandex-team.ru/arc_vcs/market/idx/export/awaps/prepare_partition/utils/genarate_category_to_part.py
(https://paste.yandex-team.ru/4485062). Он создаст файл с описанием частей ( категория-> имя файла ). Имя конфига вшито в файл.
Также надо положить файл с именами категорий category_small.json. На основе таблицы категорий (экспортнуть её в YSON, достаточно полей "hyper_id", "uniq_name")

Пример

```
./prepare-partition  \
-o feeds_smart_config.json \                                       # выходной конфиг (одна чать)
-s 50000 \                                                         # размер который мы хотим
-f "custom_label_category_id" \                                    # по этому полю oоффера будет делиться (уже в работе, на проде)
-n 0 \                                                             # нуменорать части с 0 (дефаулт)
-d \                                                               # включить доп обработку
-g hid_catstream.json \                                            # мапинг категорий на группы
-i https://server.mds/market_k50-beru-beru_offers-full-all-part-rus-avto-1.xml \  # набор имен имя старых фидов (на их строим статистику)
https://server.mds/market_k50-beru-beru_offers-full-all-part-rus-avto-2.xml
https://server.mds/market_k50-beru-beru_offers-full-all-part-rus-bytovaya_tekhnika-1.xml
https://server.mds/market_k50-beru-beru_offers-full-all-part-rus-dacha_sad_i_ogorod-1.xml
https://server.mds/market_k50-beru-beru_offers-full-all-part-rus-detskie_tovary-1.xml
...
```
старые скрипты для работы по часятм (https://paste.yandex-team.ru/4485062 ; https://paste.yandex-team.ru/4484129 )
