# Image new runtime tools
**make_ratings_file** - утилита для генерации ratings.tsv файлика из таблички-пула обучения группы качества

**rebuild_embeddings** - утилита для быстрого перестроения эмбеддингов для построенного индекса

**create_trie** - утилита для создания трая с докидами, используется в подгтовке пула - в трай складываются докиды треша

**nn_create_pool** - утилита для подготовки пула обучения модели эмбеддингов, используется в графе подгтовки пула  нирване

**train_model** - обучение модели эмбеддингов, запускается в графе обучения модели в нирване

**train_helper** - вспомогательная утилита для обучения
    **CreateTrie** - режим для создания трая с докидами, используется в подгтовке пула - в трай складываются докиды треша

**convert_tf2nn_json**

**scripts/add_options_to_json_3.py** - хелпер, патчит json-описание параметров обучения модели настройками из графа



# Документация
https://wiki.yandex-team.ru/users/temnajab/Konvejjer-obuchenija-novogo-rantajjma-kartinok/


## TODO-list для добавления экспериментальных факторов и эмбеддингов в продакшн
1. Обновить константу для продакшн факторов [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/images/kernel/new_runtime/doc_factors/fill_factors.cpp?rev=r8094768#L25)
2. Вынести из-под флага isExperimental соответствующие факторы и эмбеддинги [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/images/kernel/new_runtime/doc_factors/fill_factors.cpp?rev=r8094768#L570)
* Еще конкретно для дистиллированного берта: дописать код для BertDistill в среднем (подробнее в IMAGES-17821)
3. Добавить флаг для включения подтягивания embedding ranges из прото описания модели вместо вхардкоженных (сначала в experimental shardwriter при обучении и тестировании, потом в прод уже нужно в просто shardwriter)


