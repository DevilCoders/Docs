# Робокотов

Микросервис для оперативных и **небольших** отчетов с отбивками в телеграм

## Get started
1. `ya make`
2. `robokotov --help`
3. `robokotov -c config.yaml runserver`

##  Добавить новый склад

```(bash)
curl -XPUT https://robokotov.vs.market.yandex.net/v1/warehouse_properties -d'{"ID":171,"Name":"Томилино","DBHost":"sql-tom.mast.yandex-team.ru","DBPort":1433,"DBUser":"","DBPassword":"","SolomonServiceName":"tomilino"}'
```

##  Добавить склад в отчет по наполняемости (ordersIPO)

```(bash)
curl -XPUT https://robokotov.vs.market.yandex.net/v1/order_ipo -d'{"WarehouseID":300,"TGChatList":"79428378,XXX","DaysForward":5}'
```

##  Добавить склад в информирование о созданных заказах (orderCreated)
```(sql)
INSERT INTO public.order_created_job (warehouse_id, tg_chat_id) VALUES (330, 79428378);
```

## swagger
1. swagger.yaml - описание
2. /docs - swagger UI c описанием API
