Хранение архива склейки
=======================

Хранит таблицы в зависимости от параметров конфигурации с прореживанием и с дельта кодированием.

Для обеспечения метрик стабильности склейки - таблица вершин хранится с ежедневной раскладкой на 33 дня.
В остальных случаях используется прореживание "недельное" и "месячное".

Параметры копирования указываются в директории `conf` и описываются как текстовые протобуфы.
По результатам копирования отправляется реактор событие в дерево [/crypta/graph/archive](https://reactor.yandex-team.ru/browse?selected=8126289) - задается в прото конфиге.

Запускаются из санбокс задачи [CryptaGraphHumanMatchingBackup](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/crypta/graph/matching/backup), по рассписанию или реакции.

## Диффлог

Т.к. большая часть склейки не меняется день-ото-дня, о чем подтверждают метрики стабильности идентификтаоров.
Мы можем оптимизировать потребление диска для хранения истории, за счет разделения ежедневных таблиц на пару (база + дельта).

Схема диффлога:

```bash
.../vertices_no_multi_profile/difflog
├── internal
│   ├── ...  # базовые таблицы с контентом
│   ├── 2021-01-15
│   ├── 2021-01-01
│   └── 2021-02-01
├── base
│   ├── ...  # ссылки на внутреннее представление базовой таблицы
│   ├── 2021-02-02
│   ├── 2021-02-03
│   └── 2021-02-04
└── delta
    ├── ...  # таблицы с изменившимися идентификаторами
    ├── 2021-02-02
    ├── 2021-02-03
    └── 2021-02-04
```

Каждая дельта таблица строится на базовой не зависимо от предыдущих.
**Важно**: Т.к. дельта независима - нельзя использовать кумулятивное восстановление всех дней сразу.
Это бессмысленно и может привести к некорректным результатам.

Нужно восстанавливать каждый день по отдельности.


```base
... Base 0 --+---+---+---+-- ... Base 1 --+---+---+---+-- ...
             |   |   |   |                |   |   |   |  
             d00 d01 d02 d03              d10 d11 d12 d13
```

Обновление информации об идентификаторе - переписывает его в дельта таблице.
При этом, если идентификатор был удален из склейки,
то в дельта таблице он будет записан со значением Null в целевой колонке.

Для получения полной (исходной) таблицы нужно:
 - Взять строки из базовой таблицы, такие, которые нет в дельте.
 - Взять строки из дельты, такие, которые имеют не `Null` значение по целевой колонке (cryptaId)

Пример получения финальной таблицы:

Способ восстановления (с использованием даты) https://yql.yandex-team.ru/Operations/YCpG-guEI31eQPNljfOYK-kKRDTUM7v-mR_-vXPA75U=

```sql
USE Hahn;
$base_path = "//home/crypta/archive/graph/vertices_no_multi_profile";

DEFINE SUBQUERY $JoinRecover($delta, $base) AS
    $target_field = "cryptaId";

    SELECT * FROM (
        SELECT base.*
        FROM $base AS base
        LEFT ONLY JOIN $delta AS delta
        USING (id, id_type)

        UNION ALL
        
        SELECT delta.*
        FROM $delta AS delta
        WHERE TryMember(TableRow(), $target_field, NULL) IS NOT NULL
    ) ORDER BY id, id_type;
END DEFINE;

DEFINE SUBQUERY $GrouByRecover($delta, $base) AS
    SELECT id, id_type, MAX_BY(cryptaId, `date`) AS cryptaId
    FROM CONCAT(
        $delta,
        $base
    ) GROUP BY id, id_type
    HAVING MAX_BY(cryptaId, `date`) IS NOT NULL;
END DEFINE;

EXPORT $JoinRecover, $GrouByRecover;
```

Альтернативный способ восстановления https://yql.yandex-team.ru/Operations/YBhzBdK3DKj42nGhReFYgADkM_w1c8GZK-fT8OecVPU=

```sql
USE Hahn;
$base_path = "//home/crypta/archive/graph/soupy_indevice";

DEFINE SUBQUERY $JoinRecover($date) AS
    $path = $base_path || "/difflog";
    $target_field = "indevice_id";

    SELECT * FROM (
        SELECT base.*
        FROM REGEXP($path, "base", $date) AS base
        LEFT ONLY JOIN REGEXP($path, "delta", $date) AS delta
        USING (id_type, id)

        UNION ALL
        
        SELECT delta.*
        FROM REGEXP($path, "delta", $date) AS delta
        WHERE TryMember(TableRow(), $target_field, NULL) IS NOT NULL
    ) ORDER BY id_type, id;
END DEFINE;

DEFINE SUBQUERY $GrouByRecover($date) AS
    $path = $base_path || "/difflog";

    SELECT id, id_type, MAX_BY(indevice_id, `date`) AS indevice_id
    FROM REGEXP($path, "(base|delta)", $date) AS base
    GROUP BY id_type, id
    HAVING MAX_BY(indevice_id, `date`) IS NOT NULL;
END DEFINE;

DEFINE ACTION $Assert($date) AS
    $etalon = $base_path || "/daily/" || $date;
    $etalon_c = SELECT COUNT(1) FROM $etalon;
    $Join_c = SELECT COUNT(1) FROM $JoinRecover($date);
    $GroupBy_c = SELECT COUNT(1) FROM $GrouByRecover($date);

    DISCARD SELECT Ensure(
        Null, ($etalon_c == $Join_c) AND ($Join_c == $GroupBy_c),
        String::JoinFromList(
            AsList(
                "Miss Rows e=",
                CAST($etalon_c AS String),
                " j=",
                CAST($Join_c AS String),
                " g=",
                CAST($GroupBy_c AS String)
            ), ""
        )
    );

    $Join_Eq = (
        SELECT COUNT(1)
        FROM $etalon AS e
        INNER JOIN $JoinRecover($date) AS r
        USING (id_type, id, indevice_id)
    );

    $GroupBy_Eq = (
        SELECT COUNT(1)
        FROM $etalon AS e
        INNER JOIN $GrouByRecover($date) AS r
        USING (id_type, id, indevice_id)
    );

    DISCARD SELECT Ensure(
        Null, ($etalon_c == $Join_Eq) AND ($Join_c == $GroupBy_Eq),
        String::JoinFromList(
            AsList(
                "Uncover Error e=",
                CAST($etalon_c AS String),
                " j=",
                CAST($Join_Eq AS String),
                " g=",
                CAST($GroupBy_Eq AS String)
            ), ""
        )
    );

END DEFINE;

EXPORT $JoinRecover, $GrouByRecover, $Assert;
```
