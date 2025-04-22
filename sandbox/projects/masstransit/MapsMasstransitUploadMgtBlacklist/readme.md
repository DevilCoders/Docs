Эта задача загружает черный список для расписаний МГТ в огород. Подробнее про подклейку расписаний МГТ написано на вики: https://wiki.yandex-team.ru/maps/dev/core/masstransit/data/MGT/

Задача автоматически запускается [testenv'ом](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/maps/masstransit/UploadMgtBlacklist.yaml) на каждый коммит в файл https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/configs/mgt_blacklist/blacklist.txt.

## Как релизить код задачи
В продакшене задача запускается как бинарная. Задача автоматически выбирает самый новый ресурс с бинарем. Бинарь надо собирать задачей DEPLOY_BINARY_TASK. Ресурсу с бинарем нужно проставить атрибуты release: stable (NB: не released, т.е. зарелизить задачу стандартной кнопкой не прокатит) и task_type: MAPS_MASSTRANSIT_UPLOAD_MGT_BLACKLIST. Можно просто склонировать вот эту задачу https://sandbox.yandex-team.ru/task/488409820/view и поменять ревизию в параметрах.

Перед тем как собирать релиз с атрибутом stable, можно сначала собрать без этого атрибута и вручную запустить задачу MAPS_MASSTRANSIT_UPLOAD_MGT_BLACKLIST с получившимся ресурсом, чтобы проверить, что все работает как надо. Для этого при запуске MAPS_MASSTRANSIT_UPLOAD_MGT_BLACKLIST нужно выставить параметр binary_executor_release_type в custom, чтобы она использовала тот бинарь, который указали, а не последний доступный релиз.