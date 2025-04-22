### Вариант с использованием SQL запроса

```python
import spyt
import pyspark.sql.functions as F
import pyspark.sql.types as T
from pyspark.sql.functions import col, lit, broadcast

spark = spyt.connect()

spark.read.yt("//home/taxi-dwh/summary/dm_order/2020-05").registerTempTable("dm_order")
spark.sql("""
SELECT country,
       application_locale,
       COUNT(*) AS cnt
FROM dm_order
GROUP BY country, application_locale
ORDER BY country ASC, cnt DESC
""").toPandas()
```

### И использованием Spark DataFrame API

```
import spyt
import pyspark.sql.functions as F
import pyspark.sql.types as T
from pyspark.sql.functions import col, lit, broadcast

spark = spyt.connect()

spark.read.yt("//home/taxi-dwh/summary/dm_order/2020-05") \
    .groupBy("country", "application_locale") \
    .agg(F.count("*").alias("cnt")) \
    .sort(col("country"), F.desc("cnt")) \
    .toPandas()
```
