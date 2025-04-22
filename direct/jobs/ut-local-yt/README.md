#### FAT-тесты

Здесь предполагается собирать тесты, время сборки и/или выполнения которых велико.
Пока что под эту категорию попали тесты, работающие с локальным YT из рецептов.

##### Рецепты и YT

Идея была описана здесь https://clubs.at.yandex-team.ru/arcadia/15669

Ещё описание здесь https://wiki.yandex-team.ru/yatool/test/recipes

В целом, для написания теста теперь достаточно добавить инклуд рецепта в ya.make, и
во время выполнения теста получить координаты YT из переменных окружения YT_PROXY и YT_RPC_PROXY.

Однако, это драматически влияет на время сборки и размер артефактов в .ya (из-за добавления Yt в зависимости).
Поэтому, чтобы не усложнять жизнь обычным тестам, было решено их положить отдельно как FAT-тесты.

##### Локальный запуск

Из-за увеличившегося времени сборки запустить локально эти тесты проблематично. Но, в принципе,
это возможно, если есть свободные 40ГБ места в `.ya`. Но всё же проще делать это на дев-машинках.

##### Запуск на ppcdev

Можно счекаутить аркадию (`direct-mk java-init -- -a jobs`), пойти в директорию direct/jobs/local_yt_ut и выполнить

```
# увеличить лимит виртуальной памяти
ulimit -v 100000000
# счекаутить все необходимые зависимости
../../../ya make --checkout -j0 -tA .
# собрать и запустить тесты
../../../ya make -tA --show-passed-tests '--test-filter=ru.yandex.direct.core.entity.bs.PhraseIdByDataMd5RepositoryTest::*'
```

##### Отладка на ppcdev

```
ulimit -v 100000000
../../../ya make -tA --show-passed-tests '--test-filter=ru.yandex.direct.core.entity.bs.PhraseIdByDataMd5RepositoryTest::*' '--jvm-args=-agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=5115' --test-disable-timeout
```

Потом выполнить Forward Ports на ppcdev1 и подключиться Идеей.

##### Рецепт YT_LOCAL на ppcdev, а запуск и отладка локально

Удобнее всего запустить тест на ppcdev в режиме suspend=y, но не подключаться к нему, а найти координаты
YT и далее запускать тесты уже локально.

```
ulimit -v 100000000
../../../ya make -tA --show-passed-tests '--test-filter=ru.yandex.direct.core.entity.bs.PhraseIdByDataMd5RepositoryTest::*' '--jvm-args=-agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=5115' --test-disable-timeout
```

далее нужно найти номера портов, которые слушают YT прокси: http и rpc.
Для этого можно посмотреть процессы вашего пользователя:

```
ps aux | grep $(whoami) | grep -v run_test | grep 'ytserver-http-proxy\|ytserver-proxy'
gukserg   105056  7.6  0.1 11689156 265224 ?     SNsl Jul24  87:50 ytserver-http-proxy --legacy-config /home/gukserg/.ya/build/build_root/10mc/0001bb/direct/intapi/fat_ut/test-results/intapi-fat_ut/testing_out_stuff/yt_wd/1e324fd9-e8fc-4871-8c46-78213068b3cf/configs/http-proxy-0.json
gukserg   105104  4.3  0.0 11615480 206588 ?     SNsl Jul24  50:29 ytserver-proxy --pdeathsig 9 --config /home/gukserg/.ya/build/build_root/10mc/0001bb/direct/intapi/fat_ut/test-results/intapi-fat_ut/testing_out_stuff/yt_wd/1e324fd9-e8fc-4871-8c46-78213068b3cf/configs/rpc-proxy-0.yson
```

и в них найти yt proxy обоих видов. В строке запуска к ним будут пути к json/yson конфигам.
Один из них будет про http proxy, один -- про rpc proxy. Для http proxy порт будет в поле
```
"port": 12345
```
для rpc proxy в поле
```
"rpc_port" = 54321;
```

Работоспособность http proxy проверить проще всего:

```
YT_PROXY=localhost:12345 yt list //tmp
```

Rpc proxy так проверить не удастся, нужно запустить какой-нибудь тест (например, `smokeYtTest`), предварительно задав для него переменную окружения
```
YT_PROXY=localhost:12345
```

Естественно, нужно не забыть сделать Port Forwarding перед тем, как пробовать использовать
эти порты с локальной тачки.

```
ssh -L 12345:localhost:12345 ppcdev1
ssh -L 54321:localhost:54321 ppcdev1
```


UPD: Теперь RPC прокси дискаверятся автоматически, через HTTP-прокси. И поэтому адреса, к которым клиент будет
пытаться подключиться, будут вида ppcdev1.yandex.ru:45678. Чтобы это работало, можно временно локально указать
в /etc/hosts, что ppcdev1.yandex.ru -- это 127.0.0.1
