#  Как поднять свой BIATHLON?

#### 1. Готовим sport_proxy.data

```
cd $ARCADIA/yweb/freshness/scripts/sport_wizard && ya make -r

# На dev-машинах скипаем инфу про билеты, т.к. ручка не доступна. На выходе получаем файлы biathlon.data и sport_proxy.data.
./create_sport_data --skip_tickets_data
```

#### 2. Собираем бинарник

```
cd $ARCADIA/extsearch/wizards/sport_proxy/bin
ya make -r
```

#### 3. Подкладываем к бинарнику data-файлы

```
cp $ARCADIA/yweb/freshness/scripts/sport_wizard/sport_proxy.data .

rsync rsync://sandbox-storage25.search.yandex.net/sandbox-resources/62/84/162366284/geodb.data geodb.data
# geodb.data из этого таска: https://sandbox.yandex-team.ru/task/69993310/view
```

#### 4. Запускаем

```
./sport_proxy sport_proxy.cfg
```

# Как сходить в свой BIATHLON?

```
&srcrwr=BIATHLON:<hostname>:<apphost-port>:<timeout>
```
Пример:
```
https://yandex.ru/search/?text=лига+чемпионов&lr=213&srcrwr=BIATHLON:devtools-yt24.search.yandex.net:17045:1000000

# В данном случае бета источника BIATHON поднята на хосте devtools-yt24.search.yandex.net
# 17045 - порт из конфига sport_proxy.cfg из секции Apphost
```
