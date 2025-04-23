# Direct
Построение подмножества склейки по прямым и строгим связкам с разбиением на таблицы по типам идентификаторов с созданием публичных линков (//home/crypta/public/) на них и созданием линков на суповые таблицы и таблицы домохозяйств

### CI

This package is automatically built by TestEnv: 
https://beta-testenv.yandex-team.ru/project/crypta/job/BUILD_CRYPTA_GRAPH_TASK_RUNNER/history?limit=20

## Построение 
Построение связок происходит поверх склейки [edges_by_crypta_id](https://yt.yandex-team.ru/hahn/?page=navigation&path=//home/crypta/production/state/graph/v2/matching/edges_by_crypta_id).

### Честный директ
Соседние по склейке вершины.

При таком подходе получается недостаточный охват, поэтому мы рассматриваем соседей по строгим-компонентам.
### Расширенный строгими ребрами директ
Построение расширенных соседей для вершины $v$ происходит в три этапа:

[1)](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/matching/direct/lib/native/direct.cpp?rev=r7047352#L259) 
обход по строгим ребрам рекурсивно 
$N_1 = Strict(v)$

[2)](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/matching/direct/lib/native/direct.cpp?rev=r7047352#L260) 
шаг один по всем ребрам
$N_2 = Neighbours(N_1)$

[3)](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/matching/direct/lib/native/direct.cpp?rev=r7047352#L262) 
снова строгие рекурсивно
$Result = Strict(N_2)$

## Output
В выходную табличку by_id/[id1Type]/direct/[id2Type] записываются пары вершин, если
1) id1Type, id2Type определен в [proto/public_edges.pb.txt](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/matching/direct/proto/public_edges.pb.txt?rev=r7047352)
2) вторая вершина находится в (расширенных строгими) соседях первой
