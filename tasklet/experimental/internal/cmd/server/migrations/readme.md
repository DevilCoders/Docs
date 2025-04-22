## Миграции

### Настройка

Создаём профайлы для нужных баз

```shell
ya ydb config profile create my_database
ya ydb config profile create testing_database
```

### Делаем бекап и проверяем миграцию

1. Бекап

```shell
sandbox=~/migrate_v1
mkdir $sandbox
cd $sandbox
ya ydb -p testing_database  tools dump  -p sbx_dev/
```

2. Восстанавливаем базу

```shell
cd $sandbox
ya ydb  -p my_database  tools restore -p dbv1 -i backup_20220622T170332/ --rps 1000 --upload-batch-bytes 1MiB
```

3. Патчим (выставляем правильный folder) конфиг и накатываем миграцию

```
./tasklet-server -b alximik storage migrate
```

### Выкладка дальше

1. выкатываем бекенд. Он не будет работать, пока версия базы не верна
2. накатываем миграцию
