# Регулярные процессы, которые пушат в селфсервис (partner.vh.yandex.ru/) и видеохаб (vh.yandex.ru)

## Селфсервис (partner.vh.yandex.ru)

Хитман-процесс: https://hitman.yandex-team.ru/projects/strm_stats/vhds_reducer  
Граф: https://beta.nirvana.yandex-team.ru/flow/6c91d4d7-2bf3-4ee0-b729-e140fb2c6d59/cedbda29-d577-464e-b61b-b098b291d8e8/graph

Код в [vhds_stats_regular.py](https://a.yandex-team.ru/arc/trunk/arcadia/analytics/videolog/strm-stats/strm_cube_2/ugc_stats_regular/vhds_stats_regular.py) проверяет, появились ли новые сессии, и если да, то перекладывает их в формат СС, после этого кладёт в output_json джейсонку со списком обработанных дат. После этого кубик [upsert to ch +retries](https://beta.nirvana.yandex-team.ru/flow/6c91d4d7-2bf3-4ee0-b729-e140fb2c6d59/cedbda29-d577-464e-b61b-b098b291d8e8/graph/FlowchartBlockOperation/28dfb0ad-8a12-4e3e-9e51-def281b5c082) пушит созданные таблички в кликхаус.

## Видеохаб (vh.yandex.ru)

Процесс аналогичен предыдущему, 

Хитман-процесс: https://hitman.yandex-team.ru/projects/strm_stats/ugc_stats_regular  
Граф: https://beta.nirvana.yandex-team.ru/flow/1feff96a-0732-4273-b472-90c31764d5aa/1c6afde3-1c1e-4aea-855c-6ae123c66c63

[Кубик](https://beta.nirvana.yandex-team.ru/flow/1feff96a-0732-4273-b472-90c31764d5aa/1c6afde3-1c1e-4aea-855c-6ae123c66c63/graph/FlowchartBlockOperation/83c40132-8311-4da0-a0e4-9030dd674982) с [ugc_stats_regular.py](https://a.yandex-team.ru/arc/trunk/arcadia/analytics/videolog/strm-stats/strm_cube_2/ugc_stats_regular/ugc_stats_regular.py) перекладывает данные в формат кликхауса ВХ, [ugc upsert to ch](https://beta.nirvana.yandex-team.ru/flow/1feff96a-0732-4273-b472-90c31764d5aa/1c6afde3-1c1e-4aea-855c-6ae123c66c63/graph/FlowchartBlockOperation/8895ea58-9828-410b-9f42-261b1a423289) пушит.

Если падают yql-запросы, в stdout есть ссылки на них, можно открыть и посмотреть — возможно, падает [Ensure](https://a.yandex-team.ru/arc/trunk/arcadia/analytics/videolog/strm-stats/strm_cube_2/ugc_stats_regular/ugc_stats_regular.sql?rev=6919108#L147) — это значит, что в ugc-базе появился новый сервис, который нужно внести в [serviceEnum](https://a.yandex-team.ru/arc/trunk/arcadia/analytics/videolog/strm-stats/strm_cube_2/ugc_stats_regular/ugc_stats_regular.sql?rev=6919108#L81), закоммитить и перезапустить граф. В остальном, если проблема не в сети, надо призвать меня (pecheny@) или, если я недоступен, лезть смотреть в код.