Помимо GUI управлять квотами и аккаунтами можно при помощи CLI тула

CLI: [maps/infra/quotateka/cli](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/quotateka/cli/bin)

Ниже простой сценарий в качестве примера.

Проверяем состояние квот нового клиента `maps-core-teapot` 
```
$ bin/quotateka --abc=maps-core-teapot quota info
┌ maps-core-teapot ───────────────────────┬───────────────────────────┐
│           │ core-bicycle-router:general │ core-bicycle-router:heavy │
├───────────┼─────────────────────────────┼───────────────────────────┤
│     total │        0 of 540000          │          0 of 50          │
└───────────┴─────────────────────────────┴───────────────────────────┘
```
Видим выданную квоту на два ресурса в провайдере велороутер

Создаем новый аккаунт
```
$ bin/quotateka --abc=maps-core-teapot account create bike-acc --provider=core-bicycle-router
Will create new account bike-acc for maps-core-teapot
Proceed to creation? [y/N]: y

$ bin/quotateka --abc=maps-core-teapot account infro 
Account bike-acc                 
Description: -                    
TVM:                              
  --
```

Отрезаем немного квоты в новый аккаунт 
```
$ bin/quotateka --abc=maps-core-teapot quota set bike-acc core-bicycle-router:general:100000
┌ maps-core-teapot ──────────────────────┐
│          │ core-bicycle-router:general │
├──────────┼─────────────────────────────┤
│ bike-acc │          0 -> 100000        │
├──────────┼─────────────────────────────┤
│   total  │    0 -> 100000 of 540000    │
└──────────┴─────────────────────────────┘
Proceed to update? [y/N]: y
Set bike-acc core-bicycle-router:general quota to 1

$ bin/quotateka --abc=maps-core-teapot quota info
┌ maps-core-teapot ───────────────────────┬───────────────────────────┐
│           │ core-bicycle-router:general │ core-bicycle-router:heavy │
├───────────┼─────────────────────────────┼───────────────────────────┤
│     total │           100000            │             0             │
├───────────┼─────────────────────────────┼───────────────────────────┤
│     total │      100000 of 540000       │          0 of 50          │
└───────────┴─────────────────────────────┴───────────────────────────┘
```

Привязываем к аккаунту tvm
```
$ bin/quotateka --abc=maps-core-teapot account tvm add bike-acc --tvm=2002586 --name=tvm-prod
Will add tvm id 2002586 to account bike-acc for maps-core-teapot
Proceed? [y/N]: y

$ bin/quotateka --abc=maps-core-teapot account infro 
Account bike-acc                 
Description: -                    
TVM:                              
  tvm-prod: 2002586
```

На этом все. Включаем траффик и смотрим как все работает.
