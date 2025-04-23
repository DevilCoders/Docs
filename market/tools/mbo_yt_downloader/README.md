## mbo_yt_downloader

Утилита для скачивания mbo_stuff выгрузки из YT
Теоритически делает такую же выгузку, как и data getter в таком же формате
(как в /var/lib/yandex/getter/mbo_stuff/recent/stable/models на мастере)

### Запуск
$ ./mbo_yt_downloader --server arnold --mbo_export_dir //home/market/production/mbo/export/recent --dst-dir ~/dst_dir/mbo --num_threads 10

### Время
Выгрузка models_*.pb,  parameters_*.pb, sku_*.pb и deleted_models_*.pb занимает:
* 1 тред: 30 минут
* 5 тредов: 5 минут  
* 10 тредов: 9 минут 
* 20 тредов: 8 минут
* 50 тредов: 8 минут
* 100 тредов: 7 минут

### Известные отличия от вырузки
* Не создает файлы в которых нет данных (они в data getter выгрузке занимает 4 байта и в них только MAGIC)
* Порядок следования моделей внутри .pb файла может быть не такой как в MDS

