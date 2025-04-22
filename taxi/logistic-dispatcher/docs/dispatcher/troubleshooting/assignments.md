# Решение проблем с назначениями курьеров на заказ

На данной странице собраны способы самостоятельно отладить наиболее частые проблемы, возникающие при назначении курьера на заказ.

### Посмотреть все розыгрыши, в которых участвовал определенный курьер или заказ

Логи отгружаются в Кибану.

Все розыгрыши курьера по его dbid_uuid в тестинге можно посмотреть вот так:

```
ngroups:taxi_logistic-dispatcher_testing and driver_id:<dbid_uuid> and module:planner-contractor-edges
```

Все розыгрыши сегмента в тестинге можно посмотреть вот так:

```
ngroups:taxi_logistic-dispatcher_testing and cargo_ref_id:<segment_id> and module:planner-segment-edges
```

Для случая продакшена, надо поменять

```
ngroups:taxi_logistic-dispatcher_testing
```

на:

```
(ngroups:taxi_logistic-dispatcher_pre_stable or ngroups:taxi_logistic-dispatcher_stable)
```

Таким образом, для продакшена получаем следующие запросы.

Розыгрыши по курьеру:

```
(ngroups:taxi_logistic-dispatcher_pre_stable or ngroups:taxi_logistic-dispatcher_stable) and driver_id:<dbid_uuid> and module:planner-contractor-edges
```

Розыгрыши по сегменту:

```
(ngroups:taxi_logistic-dispatcher_pre_stable or ngroups:taxi_logistic-dispatcher_stable) and cargo_ref_id:<segment_id> and module:planner-segment-edges
```

### Посмотреть все назначения, сделанные Диспатчем на курьера или заказ

Логи отгружаются в Кибану. Можно поискать по логам следующим запросом:

```
ngroups:taxi_logistic-dispatcher_testing and cargo_ref_id:<segment_id> and module:planner-assignment
```

Аналогично, для продакшена:

```
(ngroups:taxi_logistic-dispatcher_pre_stable or ngroups:taxi_logistic-dispatcher_stable) and cargo_ref_id:<segment_id> and module:planner-assignment
```

### Посмотреть список всех ждущих прихода Lookup пропозишенов

Есть два способа.

Через ручку в тестинге:

```
curl "http://logistic-dispatcher.taxi.tst.yandex.net/api/proposition/list"
```

И через базу в тестинге и продакшене. Для этого, надо иметь доступ к базе Логистическго Диспатча хотя бы на чтение.

```
select * from route_propositions;
```

## FAQ

### Как узнать свой dbid_uuid?
Перейти в админку ([тестинг](https://tariff-editor.taxi.tst.yandex-team.ru/show-driver)/[продакшен](https://tariff-editor.taxi.yandex-team.ru/show-driver)). Ввести номер телефона в поле "Номер телефона". Поискать, перейти на карточку интересующего водителя.

Там нас интересуют значения полей db_id и Uuid. Берем их и записываем через подчеркивание. Сначала db_id, потом Uuid. Получаем требуемый идентификатор.

### У меня есть claim_id. Как по нему получить segment_id?
Это можно сделат, перейдя в админку cargo ([тестинг](https://tariff-editor.taxi.tst.yandex-team.ru/corp-claims)/[продакшен](https://tariff-editor.taxi.yandex-team.ru/corp-claims)), и введя его в поле "Claim ID". Появится заказ, в который нужно зайти, промотать вниз, найти секцию "segments", раскрыть ее и увидеть в поле segment_id требуемый идентификатор.

Если секция Segments пуста, то это значит, что заказ не был подтвержден отправителем.

### Мой курьер должен был получить заказ, а не получил. Почему?

Здесь описание ведется для случая тестинга.
Надо проверить следующие вещи:

#### Заказ появился в админке cargo и его статус не "Ошибка оценки"

Проверить можно в [админке](https://tariff-editor.taxi.tst.yandex-team.ru/corp-claims).

Если заказа нет, значит сломана интеграция сервиса-заказчика и сервиса cargo.

#### Курьер есть в candidates

Сначала получаем TVM-токен в candidates:

```
ya tool tvmknife get_service_ticket sshkey -q -s 2013636 -d 2014778
```

Если что-то не работает, почитать про утилиту ya и ее настройку можно [здесь](https://wiki.yandex-team.ru/yatool/).

Затем получаем профиль курьера:

```
curl -v "http://candidates.taxi.tst.yandex.net/profiles" -H "X-Ya-Service-Ticket: <результат ya tool tvmknife ...>" -H "Content-Type: application/json" --data '{"data_keys": ["eats_shift"], "driver_ids": [{"dbid": <dbid>, "uuid": <uuid>}]}'
```

В общем случае надо проверить, что позиция не (0, 0). Если это так, скорее всего, дело в том, что вы находитесь внутри здания. Используйте Fake GPS как вариант решения.

Для случая Еды, также стоит проверить, что курьер находится на смене (секция eats_shift существует и не пуста), и смена в статусе in_progress. Если это не так (в ответе вообще нет секции eats_shift, eats_shift.status не in_progress), то вы не находитесь на смене Еды, и будете с очень маленьким приоритетом получать едовые заказы.

#### Курьер находится в order_search

Берем координату из предыдущего запроса и вставляем в этот:

```
curl -v "http://candidates.taxi.tst.yandex.net/order-search" -H "X-Ya-Service-Ticket: <результат ya tool tvmknife ...>" --data '{"point": <координата из прошлого запроса>, "max_distance": 1000, "limit": 5}' -H "Content-Type: application/json"
```

Надо проверить, что курьер с требуемым dbid_uuid придет в ответе ручки.

Если дело касается заказа Еды, запрос можно расширить:

```
curl -v "http://candidates.taxi.tst.yandex.net/order-search" -H "X-Ya-Service-Ticket: <результат ya tool tvmknife ...>" --data '{"point": <координата из прошлого запроса>, "max_distance": 1000, "limit": 5, "eats_shift": {"shift_required": true, "only_active": true}, "order": {"source": "eats"}}' -H "Content-Type: application/json"
```

Что приведет к тому, что искаться будут только курьеры, в данный момент находящиеся на едовой смене.

#### Курьер участвовал в розыгрышах

Идем в [кибану](https://kibana.taxi.tst.yandex-team.ru/app/kibana) и вставляем запрос:

```
ngroups:taxi_logistic-dispatcher_testing and driver_id:<dbid_uuid> and module:planner-contractor-edges
```

#### Заказ участвовал в розыгрышах

Идем в [кибану](https://kibana.taxi.tst.yandex-team.ru/app/kibana) и вставляем запрос:

```
ngroups:taxi_logistic-dispatcher_testing and cargo_ref_id:<segment_id> and module:planner-segment-edges
```

Смотрим, когда была последняя запись лога (не слишком ли давно) - возможно, розыгрыши для этого заказа уже прекратились.

Ищем своего курьера в последней записи лога в поле text. Если статус ребра для этого курьера не regular, то Диспатч пытался построить связь между ними, но из-за какой-то причины не смог это сделать. Расшифровка причин есть выше.

Если же ребра для этого курьера

#### На заказ случилось какое-то назначение

Самый простой способ это увидеть в тестинге - посмотреть на [дашборд](https://grafana.yandex-team.ru/d/oE3PPtnGz/planner?orgId=1&refresh=5s&from=now-15m&to=now) Планировщика Диспатча, в секцию Propositions Built. Если после вашего заказа на графике появился пик - на кого-то был построен маршрутный лист и, скорее всего, по вашему заказу.

#### Предложение маршрутного листа еще существует

После того, как Диспатч построил маршрутный лист, этот маршрутный лист должен быть доставлен до курьера. Для этого, Диспатч ходит в сервис cargo, который создает заказ в Такси. Этот заказ еще не имеет исполнителя. Когда заказ подходит к своему due, то есть времени подачи, сервис Lookup начинает опрашивать сервис Диспатча на предмет того, есть ли исполнитель на данный заказ. Диспатч отвечает утвердительно, если в его базе есть маршрутный лист на этот заказ.

После того, как исполнитель взял заказ, маршрутный лист исчезает из таблички route_propositions базы Диспатча.

__TL;DR: после построения маршрутного листа, заказ прилетает в Таксометр не мгновенно.__

Из этого следует, что существуют заказы, на которые маршрутные листы уже построены, но за которыми Lookup еще не пришел. Посмотреть все такие маршрутные листы вместе с курьерами можно так:

```
curl "http://logistic-dispatcher.taxi.tst.yandex.net/api/proposition/list"
```

Так как в ответе будет довольно много информации, можно проверить, что маршрутный лист существует для заданного курьера:

```
curl "http://logistic-dispatcher.taxi.tst.yandex.net/api/proposition/list" | grep <dbid_uuid>
```

Если маршрутный лист на вашего курьера существует в этой ручке, скорее всего, за ним просто не успел прийти lookup и надо просто немного подождать.
