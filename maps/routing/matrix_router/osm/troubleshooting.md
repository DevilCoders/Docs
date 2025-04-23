### Зажегся мониторинг disk_quota
Заканчивается место на одном из разделов в контейнере сервиса maps-core-driving-matrix-router-over-osm.

1. Определите раздел, на котором заканчивается место. Откройте [график занятости дискового пространства](https://yasm.yandex-team.ru/template/panel/maps-core-driving-matrix-router-over-osm-stable-panel-main/-/7/), сгенерированного SEDEM.
2. Если это - раздел /persistent, то, скорее всего, место занято датасетами yandex-maps-osm-graph-speed-profiles (они занимают достаточно много, более 100 GB - одна версия).
3. Проверьте в [координаторе экстатика](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-osm-graph-speed-profiles/versions), что слишком много версий датасетов. Версий должно быть не более трёх в обычном состоянии, в крайнем случае - четыре в момент сборки новой версии.
4. Пусть версий больше трёх и вы приняли решение удалить некоторую, чтобы освободить пространство на диске. Надо определить, откуда закачивается датасет. Смотрим [конфиг экстатика](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ecstatic/stable/driving-matrix-router-over-osm-rtc.conf?rev=r8445216#L7) и запоминаем tvm: 2028240.
5. Этот tvm соответствует сервису [osm-road-graph](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_osm_road_graph_stable/), на машине которого собирается датасет и загружается в ecstatic. Чтобы удалить датасет, нужно воспользоваться утилитой ecstatic, Это можно сделать, зайдя, например, по ssh в контейнер.
6. Определившись с версией удаляемого датасета (например, 21.08.28-0), надо выполнить команду:
```
ecstatic --tvm-id=2028240 --tvm-secret "TVM_SECRET" remove yandex-maps-osm-graph-speed-profiles=21.08.28-0
```

