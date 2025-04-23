# Blue Index Backup (blue_idx_backup)

Тулза для бекапа и публикации из бекапа синих поколений.

В режиме демона проверяет last_complete.  
Если появилось новое поколение, то копирует его с мастера и воркера на воркер.  
Директория для бекапа: ```/indexer/market/archive```.  
Для копирования используется ```skynet```.  
Для управления используется ```mif```.  

## testing (старый)
1. [Лог демона на мастере](http://mi01ht.market.yandex.net/yandex/mif/log/blue_idx_backup.log)
2. [Список поколений на воркере](http://idx-blue01ht.market.yandex.net:3131/yandex/mif/archive/)

## testing (новый)
Мастер и воркер на одном хосте.
1. [Лог демона на мастере](http://mi-blue01ht.market.yandex.net/yandex/mif/log/blue_idx_backup.log)
2. [Список поколений на воркере](http://mi-blue01ht.market.yandex.net:3131/yandex/mif/archive/)

## production:stratocaster
1. [Лог демона на мастере](http://mi01h.market.yandex.net/yandex/mif/log/blue_idx_backup.log)
2. [Список поколений на воркере](http://idx-blue01h.market.yandex.net:3131/yandex/mif/archive/)

## production:gibson
1. [Лог демона на мастере](http://mi01v.market.yandex.net/yandex/mif/log/blue_idx_backup.log)
2. [Список поколений на воркере](http://idx-blue01v.market.yandex.net:3131/yandex/mif/archive/)

## Daemon
Работает на мастер машинах индексатора: ```blue_idx_backup forever```
1. [init.d](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/marketindexer/debian/blue-idx-backup.init)

## CLI
1. Список поколений: ```blue_idx_backup ls```
2. Разложить поколение из бекапа: ```blue_idx_backup publish GENERATION```

### Help
```
manushkin@mi01ht:~$ blue_idx_backup 
Usage: blue_idx_backup [OPTIONS] COMMAND [ARGS]...

  bib is BlueIndexBackup.

Options:
  -l, --log-file TEXT
  -a, --archive-dir TEXT
  -f, --force
  -n, --dry-run
  --testing
  --production
  --stratocaster
  --gibson
  -h, --help              Show this message and exit.

Commands:
  backup   Make backup for GENERATION.
  forever  Check for new generation and make backup.
  ls       List generations for all backups.
  publish  Publish GENERATION from backup.
```
