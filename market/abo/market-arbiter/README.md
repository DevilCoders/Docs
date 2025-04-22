# Arbiter

## Что где
Релизный пайплайн:
https://tsum.yandex-team.ru/pipe/projects/abo/delivery-dashboard/arbiter

Тестинг:
https://arbiter.tst.vs.market.yandex.net

Прод:
https://arbiter.vs.market.yandex.net


База прод:
``````
jdbc:postgresql://man-s4ssr3uf4uvw86ld.db.yandex.net:6432,sas-b891julvlpct63xq.db.yandex.net:6432,vla-jql4t5uvajqtna5q.db.yandex.net:6432/market_arbiter_production?sslmode=require&sslmode=require&targetServerType=master&prepareThreshold=0&connectTimeout=1&loadBalanceHosts=true
``````
user: market_arbiter_production

password: https://yav.yandex-team.ru/secret/sec-01e7n92k81j9dyskwr6ev44q9p/explore/versions

База тестинг:
``````
jdbc:postgresql://man-m6jekerwqovbbid8.db.yandex.net:6432,sas-m7ufjorhw1co269d.db.yandex.net:6432,vla-mfy4z7u0uw72lku1.db.yandex.net:6432/market_arbiter_testing?sslmode=require&sslmode=require&targetServerType=master&prepareThreshold=0&connectTimeout=1&loadBalanceHosts=true
``````

user: market_arbiter_testing
password: https://yav.yandex-team.ru/secret/sec-01e7n92kpk0vnd8avfrwe8t9f0/explore/versions

## Локальный запуск в IDEA
Запускаем класс ru.yandex.market.arbiter.Arbiter

## API
Swagger: https://arbiter.tst.vs.market.yandex.net

## Как здесь все устроено
Arbiter это state машина которая

1) Создает и переключает сосотояния арбитража в ответ на вызовы ручек.
2) Находит и возвращает текущее состояние арбитража и переписок в ручки
3) Переключает некоторые состояния арбитража по расписанию

Вся логика того в какое состояние из какого состояния и в ответ на какое внешнее событие нужно переходить определена вот здесь
https://a.yandex-team.ru/arc/trunk/arcadia/market/abo/market-arbiter/src/main/java/ru/yandex/market/arbiter/workflow/WorkflowDispatcherImpl.java?rev=r7314549#L85

Есть внешние API которые реализует Arbiter
ArbiterController - API для ABO. Все действия асессора из UI ABO проходят через него
ServiceController - API для внешнего сервиса для которого делается арбитраж. Например для Супераппа
BusinesschatController - API для интеграции с платформой бизнес чатов. Чтобы получать сообщения из чатов которые работают через эту платформу

### Как менять и расширять API
1) Поменять соответсвующий yaml файл вот здесь
https://a.yandex-team.ru/arc/trunk/arcadia/market/abo/market-arbiter/api/src/main/openapi

2) Пересобрать проект IDEA через
```ya make ide idea```

После этого появятся методы в контроллерах и перегенеряться клиенты для API
