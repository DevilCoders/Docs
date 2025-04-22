# Match Maker
Система для приема и обработки заявок на покупку нового авто.

## Ссылки
[Сгенерированные метрики](https://grafana.vertis.yandex-team.ru/d/MoCpdrW7k/match-maker-api?orgId=1)

[Системные метрики](https://grafana.vertis.yandex-team.ru/d/system-info/system-info?orgId=1&var-datasource=Prometheus&var-job=match-maker&var-dc=All&var-window=2m&var-gc=All)

[Метрики kafka консюмера](https://grafana.vertis.yandex-team.ru/d/kafka-consumer/kafka-consumer?orgId=1&refresh=30s&var-datasource=Prometheus&var-job=match-maker-scheduler&var-topic=All&var-window=2m)

```grpcui -plaintext match-maker-api-grpc.vrts-slb.test.vertis.yandex.net:80```

Выкладка: [API](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_AutoRuExp_match_maker_api_release?mode=branches#all-projects) [Scheduler](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_AutoRuExp_match_maker_scheduler_release?mode=branches#all-projects)

Манифест деплоя: [API](https://github.com/YandexClassifieds/services/blob/master/deploy/match-maker-api.yml) [Sheduler](https://github.com/YandexClassifieds/services/blob/master/deploy/match-maker-scheduler.yml) 

База: [тест](https://yc.yandex-team.ru/folders/fooqm2o1sunm8jknjhkc/managed-postgresql/cluster/mdb31e8klplc26u5quus) [прод](https://yc.yandex-team.ru/folders/fooqm2o1sunm8jknjhkc/managed-postgresql/cluster/mdb2ud2egl2n9l45cp28)

Секреты: [тест](https://yav.yandex-team.ru/secret/sec-01dvzqne3q44jhbghzg8p54xwr/explore/versions) [прод](https://yav.yandex-team.ru/secret/sec-01dwzkf23d74w327619qeb56k0/explore/versions)

## Идея
Пользователь хочет купить новый автомобиль. 
В большинстве случаев он либо не станет звонить дилеру, а сразу поедет в салон(решаем с помощью walk-in), либо позвонит только лишь одному дилеру.

Для того, чтобы увеличить кол-во звонков и уменьшить головную боль пользователя мы позволяем ему оставить заявку на покупку авто, и ему перезвонят 3 дилера.
С каждого из звонков мы получим деньги.

## Сервисы
 - match-maker-api: grpc api
 - match-maker-scheduler: Шедулер + каффка консьюмеры

## Pipeline
 1. Пользователь оставляет заявку через форму на сайте.
 2. Заявка валидируется и сохраняется в базу
 3. Приходит шедулер и находит по этой заявке 3 дилерских оффера в соответствии с пожеланиями пользователя. В выборке учавствуют только офферы дилеров-участников программы.
 4. Для каждого найденного оффера шедулер идет в salesman, чтобы снять деньги за заявку и в telepony для создания подменника.
 5. Репортим событие создания заявки в брокер ([модель события](https://github.com/YandexClassifieds/autoru-backend/blob/master/schema-registry/proto/auto/match-maker/event_log_model.proto#L12)).
 
 Далее мониторим топик телепони в кафке на предмет состоявшегося звонка по каждому дилеру.
 Если звонок состоялся, то начинаем выдавать дилеру реальный номер пользователя, вместо подменного.
 
## Черные списки
Для борьбы с нежелательными заявками существует механизм черных списков: при получение заявки API проверяет, нет ли номера телефона из заявки в черном списке. Если номер в черном списке, API возвращает "успех", не сохраняя заявку в базу. Таким образом пользователь не знает, что он в черном списке, но заявка дилерам не отправляется. Черные списки храним в пальме: [test](https://palma.test.vertis.yandex-team.ru/dictionaries/auto/match_maker/blacklist), [prod](https://palma.vertis.yandex-team.ru/dictionaries/auto/match_maker/blacklist)

## Поиск заявок
При повторном создании заявки (одинаковые заявки можно создавать не чаще чем раз в 5 минут) мы должны исключить из поиска все офферы, которые мы находили для него в течение последних двух недель.
Для избежания конфликтов обработки заявок от одного пользователя двумя разными шедулерами мы создаем лок на пользователя в отдельной таблице.
В итоге, одновременно заявку от одного пользователя может обрабатывать только 1 шедулер.

## Модель данных
#### [Заявка](https://github.com/YandexClassifieds/autoru-backend/blob/master/schema-registry/proto/auto/match-maker/api_model.proto#L36)
Помимо протобафа храним в базе:
 - время создания
 - время последнего изменения (чтобы перезапускать обработку залипших заявок)
 - время истечения срока заявки (перестаем показывать контакты пользователя дилеру)
 - состояние(new - заявка не готова к обработке шедулером, needs_processing - заявка готова к обработке, busy - заявка обрабатывается одним из шедулеров, processed - заявка обработана)

## Хранилище
Данные храним в PostgreSQL([тест](https://yc.yandex-team.ru/folders/fooqm2o1sunm8jknjhkc/managed-postgresql/cluster/mdb31e8klplc26u5quus), [прод](https://yc.yandex-team.ru/folders/fooqm2o1sunm8jknjhkc/managed-postgresql/cluster/mdb2ud2egl2n9l45cp28)) в двух таблицах:
 - match_applications - таблица с заявками
 - processed_users_applications - таблица с локами на юзера
 
## Public-api
Некоторую часть логики берет на себя паблик апи:
 - В руче [поиска офферов](http://autoru-api-server-int.vrts-slb.test.vertis.yandex.net/swagger/?url=/api-docs#!/search/searchCars) возвращаем признак того, можно ли в данной выдаче показывать форму заявки на покупку нового авто. 
 - В ручках, которые отдают инфу для кабинета обогащаем заявки каталожными данными и вырезаем реальный номер пользователя, если необходимо.
