# attr_cache

**attr_cache** - простой кэш атрибутов узлов Кипариса, призванный сократить число запросов к YT. Под капотом - LRU-кэш.
Каждый закэшированный узел хранит таймстемп чтения, что позволяет время от времени перечитывать устаревшие части кэша.
При каждом обращении к Кипарису выполняется prefetch атрибутов соседних узлов - это достигается 1 запросом get на родительский узел. 