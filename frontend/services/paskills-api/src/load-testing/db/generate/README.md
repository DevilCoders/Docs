`main.ts` - скипт для генерации даннных для бд.
Вызов - `node xx...x/load/main.js a b c`

Где:

-   `a` - количество юзеров, которых необходимо создать
-   `b` - количество (максимальное) скиллов
-   `c` - макс. кол-во скиллов под одного юзера

После выполнения - необходимо "дочинить" слегка БД.

```sql
update skills set "logoId" = images.id from images where "logoId" is null and  skills.id = images."skillId";
```
