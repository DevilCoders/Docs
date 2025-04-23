Выкачиваем модерационную информацию с YT:
```bash
yt --proxy hahn read --table //home/maps/geoapp/goods/experimental_trash/photo_moderation_verdicts_tycoon --format json > photo_moderation_verdicts_tycoon
```

Запускаем выкачку метаданных из Аватарницы (желательно, на разработческой виртуалке из сети \_MAPS\_DEV\_RTC\_NETS\_, т.к. с них есть доступ до Аватарницы):
```bash
nohup ./photo_moderations --moderation photo_moderation_verdicts_tycoon > photo_moderations.out 2> photo_moderations.err < /dev/null &
```

Выкачка занимает около суток (21 час).

Мониторить прогресс можно, например, вот так:
```bash
tail -f photo_moderations.out
ps aux | grep photo_moderations
```

Загружаем результаты на YT:
```bash
yt --proxy hahn write --table '<schema=[{name = photo_link; type = string}; {name = moderation_result; type = string}; {name = exists; type = boolean}; {name = md5; type = string}; {name = crc64; type = string}; {name = modification_time; type = int64}; {name = orig_format; type = string}; {name = orig_orientation; type = string}; {name = orig_size_bytes; type = int64}; {name = orig_size_x; type = int64}; {name = orig_size_y; type = int64}]>//home/geoapp/geosearch/goods/experimental_trash/photo_moderation_hashes' --format json < out.dat
```
