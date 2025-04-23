## Picrobot
Микросервис для скачивания картинок из оферного хранилища и загрузки их в аватарницу

## Дашборд:
[https://monitoring.yandex-team.ru/projects/market-picrobot/dashboards/monmu48kr3prq8jrtg0p?range=1d&refresh=60&p.namespace=%2A](https://monitoring.yandex-team.ru/projects/market-picrobot/dashboards/monmu48kr3prq8jrtg0p?range=1d&refresh=60&p.namespace=%2A)

Cостояние очередей внутри пикробота можно посмотреть в [комунальном queue daemon](https://solomon.yandex-team.ru/?project=big_rt_queue_daemon&dashboard=queue_lags_and_rate&cluster=markov&l.consumer=processor&l.queue=%2F%2Fhome%2Fmarket%2Fproduction%2Findexer%2Fpicrobot%2Fqueues%2Finput_queue&b=1d&e=) (выбрав нужную очередь)

## Мониторинг:
[https://juggler.yandex-team.ru/raw_events/?query=tag%3Ddatacamp-picrobot](https://juggler.yandex-team.ru/raw_events/?query=tag%3Ddatacamp-picrobot)

## Схема работы
![](https://jing.yandex-team.ru/files/egorshelk/picrobot1.svg)

Пикробот состоит из нескольких независимых процессов, запущенных одновременно на каждом инстансе в няне. Процессы независимы друг от друга и общаются между собой через QYT (упорядоченные динамические таблицы на YT)
Таблицы можно найти:
* [Таблицы тестинга](https://yt.yandex-team.ru/pythia/navigation?path=//home/market/testing/indexer/picrobot)
* [Таблицы прода](https://yt.yandex-team.ru/markov/navigation?path=//home/market/production/indexer/picrobot)

### Resharder
* Читает сообщения логброкеров, сообщения приходят нескольких видов:
  * Нужен mds-json соответствующий картинки с таким урлом оригинала в таком-то mds-namespace, результат нужно сообщить для такого-то оффера
  * Результат загрузки изображения в аватарницу
* Читает QYT и статические таблицы с hahn с сообещниями-событиями (TEventMessage).

Из прочитанных сообщений достает урл изображения, канонизирует урл, определяет номер шарда и записывает в соответствующий шард QYT.

### Processor
Обрабатывает QYT resharder-а, в которой лежат все события в перемежку. Благодаря решардеру все события относящиеся к одному урлу всегда попадают в один и тот же шард. Во время обработки BigRT поднимает стейт и обработчику доступна сохраненная в стейте информация.

Процессор обрабатывает входные события, соответствующим образом обновляет стейт и отвечает в выходные очереди:
На события запросов прокачки картинок:
 * Если уже есть информация про нужный неймспейс - просто отдает наружу нужную информацию, не изменяя стейт
 * Иначе сохраняет запрос в стейт, и отправляет запрос на скачивание картинки в Самовар (если не делал этого недавно, в зависимости от политик ретраев)
 * Если такую картинку уже скачивали, и в стейте есть информация, что такая картинка уже лежит в аватарнице, но в другом неймспейсе, процессор вместо заказа картинки в Самовар заказывает скачивание в copier, который перекладывает картинку в нужный неймспейс.

При получении события удалить картинки по ключу:
 * Создает запросы на удаления для copier
 * Удаляет информацию из mdsInfo

На события о получении mds-info: сохраняет в стейт mds-info, поднимает список inflight запросов, отвечает наружу информацию по этим запросам, забывает что такие запросы были.

### QYT2LB
Перекладывает из QYT в логброкер самовара или клиента.
Q: Почему не писать в логброкер сразу из процессора?
A: Из stateful процесса очень не просто сделать надежную запись в логброкер, если нет общих транзакций State <-> LB. Очень легко в случае каких-нибудь ошибок-ретраев получить изменившийся стейт и ничего не записать в LB. Гораздо надежнее обрабатывать в отдельной stateless компоненте, довольно легко получить at least once реализацию.

### Copier
Микросервис для работы с аватарницей. Обрабатывает два типа событий:
* Получает на вход события вида "есть картинка с таким name, id в таком неймспейсе, нужно переложить в другой неймспейс". Задает запрос в аватарницу "нужно залить картинку в целевой неймспейс, данные брать по такому урлу", где урл данных это /orig картинки в другом неймспейсе.
* Получает на вход события вида "удали из аватарницы картинки для такого то namespace, group id, id".

### picrobot_http
Микросервис для обработки http запросов. Поддерживает:
* GET /state?url=<url> - отдает json с состоянием picrobot по ключу <url>
* POST /market/put_picture?url=<url> - загрузить картинку в аватарницу c ключем <url> (используется в stroller)
* POST /shops/<shop_id>/pictures - загрузить картинку в аватарницу (замена ручки строллера с тем же интерфейсом, чтобы ходить в пикробот напрямую без участия строллера)
* POST /state - отдает json со списком состояний picrobot по набору ключей из тела запроса: ["1.jpg","2.jpg"]
* Для GET и POST запросов в /state доступен режим ?format=protobuf, возвращающий соответственно [TPicrobotState](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/picrobot/processor/proto/state.proto?rev=users%2Fgbrun%2FMARKETINDEXER-43812_add_proto_response#L41) и [TPicrobotStateBatch](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/picrobot/processor/proto/state.proto?rev=users%2Fgbrun%2FMARKETINDEXER-43812_add_proto_response#L53). Также доступен параметр ff=fields, для указания полей которые будут добавлены в ответ.

Балансировщики:
* [http://datacamp-picrobot.vs.market.yandex.net](http://datacamp-picrobot.vs.market.yandex.net)
* [http://datacamp-picrobot.pre.vs.market.yandex.net](http://datacamp-picrobot.pre.vs.market.yandex.net)
* [http://datacamp-picrobot.tst.vs.market.yandex.net](http://datacamp-picrobot.tst.vs.market.yandex.net)

## Сервис в Ya.Deploy
* [тестинг SAS/VLA](https://deploy.yandex-team.ru/stages/testing_market_datacamp-picrobot/status/picrobot)
* [prestable SAS/VLA/MAN](https://deploy.yandex-team.ru/stages/prestable_market_datacamp-picrobot)
* [прод SAS/VLA/MAN](https://deploy.yandex-team.ru/stages/production_market_datacamp-picrobot)


## Повторные попытки скачивания
По каким-то причинам картинка может не скачаться с первого раза: хост лежит, хотели скачать слишком много картинок с одного хоста одновременно (не влезли в квоты зоры). В таком случае пытаемся скачать картинку ещё раз спустя какое-то время.
Для этого в стейте хранится время последней попытки, и время когда можно будет попробовать ещё раз.
Есть регулярный процесс, который обходит реплику стейта на hahn, находит все картинки, которые ещё не скачались, и чье время повторной попытки уже наступило, и генерирует таблицу с событиями "посмотри на картинку ещё раз" - решардер забирает эти события из таблицы, и процессор повторно заказывает в Самовар, если время переобхода действительно наступило.

Шедулеры:
* [https://sandbox.yandex-team.ru/scheduler/44869/view](https://sandbox.yandex-team.ru/scheduler/44869/view) тестинг
* [https://sandbox.yandex-team.ru/scheduler/44870/view](https://sandbox.yandex-team.ru/scheduler/44870/view) прод


## Удаление картинок
Sandbox таска регулярно обходит хранилище оферов и вычисляет список url которые есть в поле partner.original.source. Этот список редьюсится с state пикробота и вычисляется url которые есть в state но уже отсутствуют в хранилище оферов. По ним строится табличка с TEventMessage на удаление. Processor при обработке событий на удаление, будет удалять из аватарницы, только при получении повторного запроса на удаление.

Шедулеры:
[https://sandbox.yandex-team.ru/scheduler/696859/view](https://sandbox.yandex-team.ru/scheduler/696859/view) тестинг
[https://sandbox.yandex-team.ru/scheduler/696862/view](https://sandbox.yandex-team.ru/scheduler/696862/view) прод

## Бекапы state
Бекапы сохраняются на MR кластерах в YT.
* //home/market/testing/indexer/picrobot/state/backups
* //home/market/production/indexer/picrobot/state/backups

Шедулеры:
* [https://sandbox.yandex-team.ru/scheduler/471203/view](https://sandbox.yandex-team.ru/scheduler/471203/view) тестинг
* [https://sandbox.yandex-team.ru/scheduler/471204/view](https://sandbox.yandex-team.ru/scheduler/471204/view) прод

## Подготовка стейта
```
./prepare/prepare \
        --big-rt-cli ~/arc/arcadia/ads/bsyeti/big_rt/cli/big_rt_cli \
        --yt-meta-cluster markov \
        --yt-replicate-clusters seneca-sas \
        --yt-replicate-clusters seneca-vla \
        --yt-replicate-clusters arnold \
        --yt-replicate-clusters hahn \
        --base-path //home/market/production/indexer/picrobot \
        --processor-shard-count 64 \
        --other-shard-count 16 \
        --tablet-cell-bundle market-datacamp-production \
        --primary-medium 'ssd_blobs'
```
