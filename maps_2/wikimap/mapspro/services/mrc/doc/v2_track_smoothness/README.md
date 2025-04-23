### Введение
Ключевая функциональность ручек фотографий вдоль маршрута сосредоточена в функции [collectTrackPhotos](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/browser/lib/photo_api.cpp?rev=r8878368#L798).<br />
Она готовит множество фотографий вдоль маршрута.<br />
Для каждой фотографии возвращается id и [SubPolyline](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/libs/common/include/geometry.h?rev=r8878368#L72) - видимая часть маршрута.<br />
Основные этапы реализации:
- [матчинг маршрута на граф](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/browser/lib/photo_api.cpp?rev=r8878368#L811)
- [цикл по ребрам графа](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/browser/lib/photo_api.cpp?rev=r8878368#L825) внутри которого ищутся фотографии, покрывающие ребра

### Проблема
Для [поиска фотографий](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/browser/lib/photo_api.cpp?rev=r8878368#L645) вдоль ребер используется датасет yandex-maps-mrc-graph[-pro].<br />
В нем содержится [покрытия ребер](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/libs/fb/include/common.h?rev=r8979070#L20) самыми свежими снимками.<br />
Снимок в конце одного ребра может быть в правом ряду, а следующее ребро за левым поворотом.<br />
Такие сочетание фотографий вдоль маршрута могут быть неприятными на сложных развилках.<br />


### Предложение
- отказаться от поиска покрытий ребер в датасете yandex-maps-mrc-graph[-pro], где множество снимков ограничено только самыми свежими
- добавить в датасет yandex-maps-mrc-photo-to[-pedestrian]-edge[-pro] обратный индекс: id ребра -> id фотографии
- искать все фотографии, покрывающие ребро, с помощью нового индекса в yandex-maps-mrc-photo-to[-pedestrian]-edge[-pro]
- множество собранных снимков всего маршрута [разбить на проезды](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/libs/common/include/algorithm/for_each_passage.h?rev=r8163939#L19)
- каждому снимку проставить приоритет из двух факторов: свежесть и кол-во снимков/ребер до конца его проезда вдоль маршрута
- внутри ребра [мержить](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/libs/common/include/geometry.h?rev=r8944557#L133) снимки, используя вышеуказанный приоритет 
