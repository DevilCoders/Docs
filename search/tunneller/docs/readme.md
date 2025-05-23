Исходный список источников был нагрепан из логов tunneller: https://paste.yandex-team.ru/401345. Здесь колонки значат: название источника из DebugInfo, стадия, количество запросов и количество неответов.
Стадии между туннеллером и скрейпером матчатся так (туннелер -> скрейпер):
> search -> SEARCH
> allfactors -> FACTORS
> fetch -> FETCH

Скрейперный FACTORS_NOT_FETCHED - это микс из `FACTORS` и `FETCH`, и используется только в legacy-режиме.

Аппхостовые источники вида `APP_HOST/blender5s@3380289/IMAGES_SUGGEST_TAGS_PROXY` сокращаются до двух уровней: `APP_HOST/IMAGES_SUGGEST_TAGS_PROXY`. Это скрывает инфу о версии графов и многоуровневой топологии, но не мешает разделять источники.
То же и с остальными источниками. Они не совсем уникальны: например, RTMR есть и под источником WEB, и под источником IMAGESP. Но в целом двухуровневое указание пути хватает для дедупликации источников, и не создаёт проблем при переездах.
DebugInfo, приходящая в скрейпер, совпадает с RequestStat, который можно увидеть в ивентлогах. Пример для среднего web: https://setrace.yandex-team.ru/ui/search/971396e1-b4a5-4ec5-9ed3-e484cab809e4/results/man1-6712.search.yandex.net:10078@WEB:15370303
Не все источники в RequestStat уникальны. Так, для средних WEB 0_Tier содержит неответы всех подысточников, кроме тир1 (сниппетные, саасные, турбо, аукс источники и тп). main содержит сумму неответов базовых платины, тир0, каллисто и самохода. В целях дедупликации такие "аггрегационные" источники лучше удалять.
Далее, тот же WEB дополнительно встречается в стате в UPPER (UPPER/WEB), куда суммируется все подысточники WEB, включая неответ самого среднего WEB. Для источников под аппхостом такие аггрегации надо игнорировать - неответы среднего и так попадают в неответы app_host/*. Для источников под UPPER на них смотреть приходится, но коллизий это не создаёт (все источники под UPPER весьма простые, и необходимости в игноре какой-то части подысточников нету)
Какие-то источники дополнительно пишут стату о неответах по каким-то шардам, например:
> YMUSIC/0-8190	Search	304255	127
> YMUSIC/0-8190	Snippet	2767	0
> YMUSIC/0_TIER	Search	2433184	761
> YMUSIC/0_TIER	Snippet	22247	0
> YMUSIC/16382-24572	Search	302973	65
> YMUSIC/16382-24572	Snippet	2424	0
> YMUSIC/1_TIER	Search	0	0
> YMUSIC/24573-32763	Search	306680	134
> YMUSIC/24573-32763	Snippet	2935	0
> YMUSIC/32764-40954	Search	304031	72
> YMUSIC/32764-40954	Snippet	2760	0
> YMUSIC/40955-49145	Search	303852	74
> YMUSIC/40955-49145	Snippet	2846	0
> YMUSIC/49146-57336	Search	304215	101
> YMUSIC/49146-57336	Snippet	2833	0
> YMUSIC/57337-65533	Search	304698	94
> YMUSIC/57337-65533	Snippet	2847	0
> YMUSIC/8191-16381	Search	302480	94
> YMUSIC/8191-16381	Snippet	2835	0
> YMUSIC/ymusic	Search	2433184	761
> YMUSIC/ymusic	Snippet	22247	0

Их сумма попадает в ymusic и в 0_TIER. Неответы по этим шардам можно смело игнорить, т.к. эта дебажная инфа нечитаема, а тот же неответ всё равно аггрегируется в источнике ymusic.