## How to build and run

Собрать и запустить
```shell script
ya make
./mbi_review run MbiReview --input "`cat input.json`" --local
```
Просмотр логов
```shell script
cat ~/.sandbox/logs/last_tasklet_run.log
```

Деплой(linux)
```shell script
ya make
./mbi_review/mbi_review sb-upload --sb-schema
```

Деплой(mac os)
```shell script
ya make --target-platform=linux
scp ./mbi_review/mbi_review {user}@braavos.market.yandex.net:/home/{user}/
ssh braavos.market.yandex.net
./mbi_review sb-upload --sb-schema
```

