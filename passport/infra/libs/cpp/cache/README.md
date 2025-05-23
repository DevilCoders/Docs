==Кэш
Библиотека создана для кэширования ответов сервера.

====Инициализация
1) надо создать TContextPtr - один на весь процесс
2) у него вызвать createCache() для каждого логически изолированного набора данных
(например, method=userinfo и method=oauth дают разные ответы)
3) вызвать метод startCleaning()

====Unistat
1) TContext::unistat отдаёт:
"cache_ctx.total_size_ahhh"
2) TCache::unistat отдаёт:
"cache." + unistatName + ".get_succeed_dhhh"
"cache." + unistatName + ".put_failed_dhhh"

====Внутреннее устройство
Для всех кэшей есть общий контекст - он следит за суммарным объём потреблённой памяти.
Потребление памяти считается по-грязному: только размеры сохраннённых объектов - без учёта расхода памяти в контейнерах.
Этот же контекст занимается регулярной очисткой памяти

Каждый кэш разбит на TTimeBasedBucket'ы, которые служат для того, чтобы очистка не мешала чтению и записи.
 *        1 2 3
 *        | | |
 * |x|...|x|x|x|...|x|
 *
 * Positions:
 * 1 - start reading here and move backwards + read from writing position
 * 2 - write here
 * 3 - clean here and move forwards
Рекомендуемое количество - 3 штуки.

Каждый TTimeBasedBucket разбит на TKeyBasedBucket'ы, которые нужны, чтобы снизить конкуренцию за мьютексы.
Вместо одной хэштаблицы есть константное количество таблиц+мьютексов.
Рекомендуемое количество - не меньше чем 1.5 * количество потоков на машине. Например, 128 шт.
