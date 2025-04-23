# UEE-TMS

сервис для обогащение данных компонентами IR

## Локальный запуск

1. Postgres поднимается автоматически
2. Подключится к dev zookeper
3. Необходимо установить mongo и создать в ней базу и пользователя:
```js
use bazinga
db.createUser({user: "bazinga", pwd: "bazinga", roles: [{role: "readWrite", db: "bazinga"}], mechanisms: ["SCRAM-SHA-1"]})
```
4. Добавить VM option:
```properties
-Dconfigs.path=${ARCADIA_ROOT}/market/ir/uee/uee-tms/src/main/properties.d
-Dlog4j.configurationFile=${ARCADIA_ROOT}/market/ir/uee/uee-tms/src/main/conf/log4j2.xml
-Denvironment=local
```
5. Добавить переменные среды
```properties
UEE_YT_TOKEN=<your_yt_oauth_token>
UEE_STAFF_TOKEN=<your_staff_oauth_token>
```

## Создание новой таски
1. Создать pojo, наследника AbstractTaskPojo
2. Создать таску, наследника WorkerTask, MetaTask или другого типа таски
3. Добавить в BusinessTaskRepository метод для получения pojo
4. Добавить в добавить маппинг в BusinessToLogicalTaskMapper
5. Добавить создание новой таски в нужную метатаску. (Самая главная таска ENRICH_OFFERS_MAIN_META_TASK)
6. Добавить инициализацию таски, как бина в TaskConfig
