# Поиск для Яндекс.Облако
* Чатик поддержки https://t.me/joinchat/ClVdbhX8Pumw1Nl9fNKk_g
## Описание
4 инсталяции:
* Внешний препрод (как альфа/тестинг)
* Внешний прод
* Внутренний тест
* Внутренний прод

Классическая структура: читаем из логброкера, превращаем в индекс документы в индексаторе, отправляем в очередь.
На проксе держим api с которым работают потребители
### Внешний прод
* Балансер https://yc-search-compute-prod.search.yandex.net
* Стенд маркетплейса https://cloud.yandex.ru/marketplace?search=ubuntu
* Поиск по ресурсам https://console.cloud.yandex.ru/ -> поиск
#### Cервисы в няне:
* Прокси [yc_search_proxy_compute_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/yc_search_proxy_compute_prod/)
* Индексатор [yc_search_indexer_compute_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/yc_search_indexer_compute_prod/) 
* Бекенд [yc_search_backend_compute_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/yc_search_backend_compute_prod/)
* Очередь общая для PS [ps_search_queue_prod_1](https://nanny.yandex-team.ru/ui/#/services/catalog/ps_search_queue_prod_1/)
#### Графики
* [Общая Панель](https://yasm.yandex-team.ru/template/panel/yc_search_common/ctype=prod/)
* [Отдельно бекенд](https://yasm.yandex-team.ru/template/panel/ps_search_backend/ctype=prod;prj=ycsearch/)
* [Лоброкер лаг по последнему чтению (простой чтения топика)](https://solomon.yandex-team.ru/?graph=auto&stack=false&project=kikimr&partition=-&service=pqtabletAggregatedCounters&user_counters=PersQueue&cluster=lbk&l.TopicPath=*&l.sensor=TimeSinceLastReadMs&l.host=*&l.OriginDC=*&b=1h&e=&l.ConsumerPath=pssearch%2Fprod%2Fyc%2Fcompute%2Fsearch-indexer)
* [Лоброкер лаг по непрочитанным сообщениям](https://solomon.yandex-team.ru/?graph=auto&stack=false&project=kikimr&partition=-&service=pqtabletAggregatedCounters&user_counters=PersQueue&cluster=lbk&l.TopicPath=*&l.sensor=MessageLagByLastRead&l.host=*&l.OriginDC=*&b=1h&e=&l.ConsumerPath=pssearch%2Fprod%2Fyc%2Fcompute%2Fsearch-indexer)
* [Шивака](https://yasm.yandex-team.ru/template/panel/Shivaka/project=personalsearch-main/)
#### Внешний препрод
* Балансер https://yc-search-compute-preprod.search.yandex.net
* Стенд маркетплейса https://cloud-test.yandex.ru/marketplace?type=compute&search=цшт
#### Cервисы в няне:
* Прокси [yc_search_proxy_yp_compute_preprod](https://nanny.yandex-team.ru/ui/#/services/catalog/yc_search_proxy_yp_compute_preprod/)
* Индексатор [yc-search-indexer-yp-compute-preprod](https://nanny.yandex-team.ru/ui/#/services/catalog/yc-search-indexer-yp-compute-preprod/) 
* Бекенд [yc_search_backend_compute_preprod](https://nanny.yandex-team.ru/ui/#/services/catalog/yc_search_backend_compute_preprod/)
* Очередь [district_search_queue_test](https://nanny.yandex-team.ru/ui/#/services/catalog/district_search_queue_test/)
#### Графики
* [Общая Панель](https://yasm.yandex-team.ru/template/panel/yc_search_common/ctype=prodtest/)
* [Отдельно бекенд](https://yasm.yandex-team.ru/template/panel/ps_search_backend/ctype=prodtest;prj=ycsearch/)
* [Лоброкер лаг по последнему чтению](https://solomon.yandex-team.ru/?graph=auto&stack=false&project=kikimr&partition=-&service=pqtabletAggregatedCounters&user_counters=PersQueue&cluster=lbk&ConsumerPath=pssearch%2Fpreprod%2Fyc%2Fcompute%2Fsearch-indexer&l.TopicPath=*&l.sensor=TimeSinceLastReadMs&l.host=*&l.OriginDC=*&b=1h&e=)
* [Лоброкер лаг по непрочитанным сообщениям](https://solomon.yandex-team.ru/?graph=auto&stack=false&project=kikimr&partition=-&service=pqtabletAggregatedCounters&user_counters=PersQueue&cluster=lbk&ConsumerPath=pssearch%2Fpreprod%2Fyc%2Fcompute%2Fsearch-indexer&l.TopicPath=*&l.sensor=MessageLagByLastRead&l.host=*&l.OriginDC=*&b=1h&e=)
* [Шивака](https://yasm.yandex-team.ru/template/panel/Shivaka/project=personalsearch-main/)
### Внутренний прод
* Балансер https://yc-search-proxy-corp.search.yandex.net
#### Cервисы в няне:
* Прокси [yc_search_proxy_corp_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/yc_search_proxy_corp_prod/)
* Индексатор [yc_search_indexer_corp_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/yc_search_indexer_corp_prod/) 
* Бекенд [yc_search_backend_corp_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/yc_search_backend_corp_prod/)
* Очередь общая для PS [ ps_search_queue_prod_1](https://nanny.yandex-team.ru/ui/#/services/catalog/ps_search_queue_prod_1/)
#### Графики
* [Общая Панель](https://yasm.yandex-team.ru/template/panel/yc_search_common/ctype=prod-internal/)
* [Отдельно бекенд](https://yasm.yandex-team.ru/template/panel/ps_search_backend/ctype=prod-internal;prj=ycsearch/)
* [Лоброкер лаг по последнему чтению (простой чтения топика)](https://solomon.yandex-team.ru/?graph=auto&stack=false&project=kikimr&partition=-&service=pqtabletAggregatedCounters&user_counters=PersQueue&cluster=lbk&l.TopicPath=*&l.sensor=TimeSinceLastReadMs&l.host=*&l.OriginDC=*&l.ConsumerPath=pssearch%2Fprod%2Fyc%2Fcorp%2Fsearch-indexer&b=1h&e=)
* [Лоброкер лаг по непрочитанным сообщениям](https://solomon.yandex-team.ru/?graph=auto&stack=false&project=kikimr&partition=-&service=pqtabletAggregatedCounters&user_counters=PersQueue&cluster=lbk&l.TopicPath=*&l.sensor=MessageLagByLastRead&l.host=*&l.OriginDC=*&l.ConsumerPath=pssearch%2Fprod%2Fyc%2Fcorp%2Fsearch-indexer&b=1w&e=)
* [Шивака](https://yasm.yandex-team.ru/template/panel/Shivaka/project=personalsearch-main/)

### Внутренний тест
#### Cервисы в няне:
* Прокси [yc_search_proxy_test](https://nanny.yandex-team.ru/ui/#/services/catalog/yc_search_proxy_test/)
* Индексатор [yc_search_indexer_test](https://nanny.yandex-team.ru/ui/#/services/catalog/yc_search_indexer_test/) 
* Бекенд [yc_search_backend_test](https://nanny.yandex-team.ru/ui/#/services/catalog/yc_search_backend_test/)
* Очередь [district_search_queue_test](https://nanny.yandex-team.ru/ui/#/services/catalog/ps_search_queue_prod_1/)
#### Графики
* [Общая Панель](https://yasm.yandex-team.ru/template/panel/yc_search_common/ctype=test/)
* [Отдельно бекенд](https://yasm.yandex-team.ru/template/panel/ps_search_backend/ctype=test;prj=ycsearch/)
* [Лоброкер лаг по последнему чтению (простой чтения топика)](https://solomon.yandex-team.ru/?graph=auto&stack=false&project=kikimr&partition=-&service=pqtabletAggregatedCounters&user_counters=PersQueue&cluster=lbk&l.TopicPath=*&l.sensor=TimeSinceLastReadMs&l.host=*&l.OriginDC=*&l.ConsumerPath=pssearch%2Ftest%2Fyc%2Fsearch-indexer&b=1w&e=)
* [Лоброкер лаг по непрочитанным сообщениям](https://solomon.yandex-team.ru/?graph=auto&stack=false&project=kikimr&partition=-&service=pqtabletAggregatedCounters&user_counters=PersQueue&cluster=lbk&l.TopicPath=*&l.sensor=MessageLagByLastRead&l.host=*&l.OriginDC=*&l.ConsumerPath=pssearch%2Ftest%2Fyc%2Fsearch-indexer&b=1w&e=)
* [Шивака](https://yasm.yandex-team.ru/template/panel/Shivaka/project=personalsearch-main/)

### Структура сервиса
На сервисе живут два подсервиса
#### Поиск для маркетплейса
Все документы хранятся в нескольких префиксах - по одному префиксу на каждый проект маркетплейса. У всех документов id имеет вид id:yc_marketplace_doc_* . Список полей динамический и прилетает в запросе на индексацию от маркетплейса. Примерный набор можно посмотреть в yc_backend/files/yc_marketplace_backend_fields.conf
Текущие префиксы для маркетплейса prefix=yc_marketplace_user
##### Индексация
Обновление индекса маркетплейса происходит как заливка целого снепшота. Поверх текущего индекса прилетают документы все сразу, все что есть в базе.
Следующим запросом старые удаляются по метке времени. Таким образом мы фактически каждый раз заливаем целый снепшот
##### Поиск   
На стороне поисковой прокси используются две ручки:
###### `/api/marketplace/search`
Находит документы по тексту + доп фильтру 
Параметры:<br>
`&offset=0 - оффсет`<br>
`&length=5 - количество элементов в выдаче` <br>
`&sort=categories_rank - сортировка по полю, опциональный параметр`<br>
`&filter=categories_id%3Arecommended+AND+language%3Aen+AND+%28type%3Acompute-image%29 - доп условие для поиска`<br>
`&text=mytext - текст для поиска, опциональный,  требует наличия параметра search_fields со списком полей где искать текст` <br>
`&search_fields=marketingInfo.name%2CmarketingInfo.description - список полей где искать текст, обязательный если пристуствует &text`<br>

Обязательно наличие либо &filter и/или &text с &search_fields 
При поиске работает учет транслитерации/раскладки
 
###### `/api/marketplace/aggregation`
По сути это /printkeys
Строит статистику по значению, скольку документов с каждым значением есть в индексе + возможность доп фильтра документов 
Параметры:<br>
`&field=publisher.id - поле по которому строить статистику`<br>
`&filter=language%3Aen+AND+%28type%3Acompute-image%29 - доп условие для аггрегации`<br>
`&text=mytext - текст для фильтрации, опциональный,  требует наличия параметра search_fields со списком полей где искать текст` <br>
`&search_fields=marketingInfo.name%2CmarketingInfo.description - список полей где искать текст, обязательный если пристуствует &text`<br>

Оба метода выведены на общую панель

#### Поиск по ресурсам облака
##### Индексация 
Пример входящего документа
```json
{
    "deleted":"",
    "service":"compute",
    "resource_type":"instance",
    "resource_id":"sadb4hbgn9c73sdg186s",
    "permission":"compute.instances.get",
    "attributes":{"hostname":"cl1bblu3u9qdot05sr39-vasya","fqdn":"cl1bblu3u9qdot05sr39-vasya.ru-central1.internal","name":"cl1bblu3u9qdot05sr39-vasya","description":""},
    "cloud_id":"a1btdskmm5ck7oif4p5p",
    "folder_id":"c1g2456mggfboq3k7tou",
    "timestamp":"2020-10-06T18:26:01.323662+00:00"
}
```

Документ в индексе сохраняется как несколько 
1) основной c `yc_doc_type:main_doc`
2) На каждый атрибут из attributes создается отдельный документ с `yc_doc_type:attributes`
3) При удалении на документ просто проставится метка `yc_deleted_time:ts` и алиас `yc_deleted` . Так как возможна гонка удаления/добавления документа через логброкер

Из примера выше в индексе будет 5 документов - основной и 4 под аттрибуты

* Префикс каждого документа это `cloud_id`
* Основной ключ для главного документа `id = cloudid + service + resource_type + resource_id`
* Основной ключ для документа атрибута `id = cloudid + service + resource_type + resource_id + attribute_name`
* У каждого документа есть permission - в момент поиска он проверяется через IAM и документ филтруется если у пользователя нет доступа

Вот тут можно посмотреть примеры документов в индексе {% code 'mail/search/yc/yc_indexer/test/resources/ru/yandex/search/yc/expected_update.json' %}

##### Поиск `/api/search`
`&cloud_id=xxx&cloud_id=yyy либо &cloud_ids=xxx,yyy` - список cloudId в которых искать <br>
`&request=xxx` - текст запроса <br>
`&debug=true` - для вывода в лог более подробной информации <br>
`&highlight=true` - отдаем подсветку или нет <br>
`хедер x-yacloud-subjecttoken` - токен для похода с ним в iam , идентифицрует пользователя, живет ограниченное время <br>

#### Поисковая прокся [ссылка на код](./yc_search_proxy)
* /logs/access.log
* /logs/full.log
#### Индексатор [ссылка на код](./yc_indexer)
Состоит из 3 модулей запущенных через мультистартер: Продюсер, ЛогброкерКонсумер, Индексатор
ЛогброкерКонсумер консумит из топика и настреливает в Индексатор, тот превращает поток в понятные сущности для бекенда и отправляет в очередь через продюсер.
Помимо стандартных access/full логов у каждого модуля, индексатор держит два лога:
* /logs/incoming-docs.log - тело влетающих в индексатор документов
* /logs/outgoing-docs.log - тело вылетающих из индексатора документов

#### Поисковой бекенд [ссылка на код](./yc_backend)

## Сборка для развертывания в Cloud
### Описание схемы
Сервис работает на виртуалках / инстанс группах в контуре облака. Деплой происходит посредством сборки кода в образ загрузочного диска.
Для бекендов для хранения данных монтируем сетевой диск и храним данные там. 
FQDN персистентны поэтому можно зафиксировать searchmap

### Инструкция 
В каждом подсервисе существует папка packer где лежат файлы для пакера с правилом сбора образа.
Для создания образа потребуется oauth токен YC_TOKEN
1) Выкачиваем jdk, https://sandbox.yandex-team.ru/resource/1444565788/view кладем в (./yc/jdk12.tar.gz)
2) Переходим в папку подсервиса - например cd yc_backend
3) Собираем код в архив ya package ./package.json (Если не в транке, делаем mv yc_search_proxy.(version).tar.gz yc_search_proxy.tar.gz))
4) Запускаем packer - packer build ./packer/packer.image.preprod.json


