# Программа для конвертирования таблицы бакетов доставки в json представление

## Назначение
Предоставить для MSTAT таблицу c json описанием бакетов доставки.
Используя ссылки на бакеты из дампов поколений можно собрать все опции доставки офера.
Таблица используется раз в сутки при сборе дампов поколений (бывшие генлоги) джобой MSTAT.

## Краткое описание
1. Предполагается запуск по крону
   - ```sudo mindexer_clt yt_upload_buckets```
   - [каждые 30 минут](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/cron/update_cron_available/src/generator.py?blame=true&rev=5151106#L771)
2. В качестве источника используется динамическая таблица оферс-робота с протобаф описанием бакетов.
3. Целевая динамическая таблица также содержит по одной строке на бакет.
4. В целевой таблице используется специальное согласованное json описание бакетов.
5. Бакеты конвертируются независимо от типа, включая самовывоз и почту.
6. Целевая таблица дополняется новыми записями с оверрайдом старых.
7. TTL записей целевой таблицы 90 дней.

## Ссылки
- [Целевая таблица](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/gibson/out/delivery/buckets/recent&offsetMode=key)
- [Таблица на входе](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/gibson/or3/delivery-calc/delivery&offsetMode=key)
- [Прикладной тикет](https://st.yandex-team.ru/MARKETINDEXER-27377)
- [Исходный проект](https://st.yandex-team.ru/MARKETINDEXER-21226)

## Использование
<pre>
```
YT_TOKEN_PATH=/etc/datasources/yt-market-indexer YT_PROXY=arnold ./bucket-joptions --yt-proxy=arnold --yt-user=robot-mrkt-idx-tst --yt-bundle=market-testing --yt-input=//home/market/testing/indexer/stratocaster/or3/delivery-calc/delivery --yt-output=//home/market/testing/indexer/stratocaster/out/delivery/buckets/recent
```
</pre>
