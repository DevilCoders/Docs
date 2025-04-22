# Самоварные обходы для Директа

## Общая схема процесса

[![samovar_bannerland](https://jing.yandex-team.ru/files/oddeye/browser_SsCWSHfitw.png)](https://jing.yandex-team.ru/files/oddeye/browser_SsCWSHfitw.png)

## Превью Смарта по сайту

Смарт баннер это красиво собранный баннер из товарного предложения и картинки. Для того, чтобы стимулировать владельца сайта пользоваться смарт баннерами, делается превью - некоторый набор смарт баннеров, которые сделаны из **полезных** офферов сайта. Превью дает возможность владельцу сайта ценивать продукт **Смарт по сайту** - видеть примеры готовых смарт баннеров и оценивать их корректность, актуальность, красоту.

## Скачивание семпла для превью Смарта по сайту

Запрос на скачивание семпла офферов сайта (хоста) отправляется в Самовар через logbroker топик [samovar/feeds-ext](https://lb.yandex-team.ru/logbroker/accounts/samovar/feeds-ext?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&metricsFrom=1648710801568&metricsTo=1648797201569&sortOrder=%22default%22). Запрос должен отправляться на главную страницу хоста - морду (например, https://yandex.ru/), и должен обозначаться строкой **datacamp-bannerland-host-check-ext** и должен содержать в себе [DCMP контекст](https://a.yandex-team.ru/arc_vcs/market/mbi/proto/SamovarContext.proto?rev=r9280743#L167). Более подробное описание по формированию запроса [находится тут](https://wiki.yandex-team.ru/robot/samovar/feedsext/). 

{% note warning %}

Запрос скачивает заранее [собранный семпл](https://a.yandex-team.ru/arc/trunk/arcadia/robot/samovar/conf/conf-primary-arnold/sampling_config.pb.txt?rev=r9287163#L42) офферов хоста, который постоянно (около раза в неделю) актуализируется Самоваром. Это означает, что один и тот же запрос может скачивать разный набор офферов.

{% endnote %}

 В запросе можно [задать максимальный размер семпла](https://a.yandex-team.ru/arc/trunk/arcadia/robot/samovar/combustor/hooks/simple/datacamp_bannerland_host_check_hook.cpp?rev=r8995045#L130). По умолчанию максимальный размер семпла равен [120](https://a.yandex-team.ru/arc/trunk/arcadia/robot/samovar/conf/conf-primary-arnold/sampling_config.pb.txt?rev=r9287163#L47).

Этот тип запроса уже используется во время регистрации хоста в MBI через Директовую ручку (https://st.yandex-team.ru/MBI-60592, https://st.yandex-team.ru/MBI-73108).


{% cut "В следующих местах могут быть проблемы с прокачкой семпла офферов для превью. Пункты указаны в порядке, который следует использовать при отладке проблем" %}

Как изучать | Колонка по центру
:--- | :---
Задание не пришло | Открываем [вьюер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer?key=https%3A%2F%2Fyandex.ru&keyType=url), вводим урл главной страницы сайта (схему http/https, а также www/www! тоже нужно учесть) и нажимаем кнопку **URL**. Ищем поле **FeedsState**, а в нем секцию **datacamp-bannerland-host-check-ext**. Если такой секции нет, значит, сингал не пришел. Так же можно собрать логи при помощи [YQL-запроса](https://yql.yandex-team.ru/Operations/YlGN7bq3kyuRPIBTqUprfhEwvXQT1HhhLd-KHRATUPc=). В них есть DCMP контекст в читабельном виде.
В задании нет DCMP контекста|Открываем [вьюер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer?key=https%3A%2F%2Fyandex.ru&keyType=url), вводим урл главной страницы сайта (схему http/https, а также www/www! тоже нужно учесть) и нажимаем кнопку **URL**. Ищем поле **FeedsState**, а в нем секцию **datacamp-bannerland-host-check-ext**, а в ней поле **FeedContext**. Если его нет, или оно пустое, то запрос пришел без контекста. Запросы также можно собрать через [YQL](https://yql.yandex-team.ru/Operations/YkfrYbq3k8maPbVypnAbgkme6-DSK0WL3rtoz16cQsM=). В логах пишется **FeedContext**.
Нет заранее собранного семпла офферов|Открываем [вьюер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer?key=https%3A%2F%2Fyandex.ru&keyType=host), вводим хост и нажимаем кнопку **HOST**. Ищем поле **SamplingData**, а в нем раздел **DataCampBannerlandOffers**. Если поля **SamplingData** или раздела **SamplingData.DataCampBannerlandOffers** нет, то, скорее всего, на хосте нет [подходящих офферов](https://a.yandex-team.ru/arc/trunk/arcadia/robot/samovar/conf/conf-primary-arnold/sampling_config.pb.txt?rev=r9287163#L43). Семплы [подходящих офферов](https://a.yandex-team.ru/arc/trunk/arcadia/robot/samovar/conf/conf-primary-arnold/sampling_config.pb.txt?rev=r9287163#L43) также выгружаются в [таблицы](https://yt.yandex-team.ru/arnold/navigation?path=//home/samovar-data/hosts_for_preview_export) в поле **Sample**.
Проверка семпла не стартовала, или стартовала, но не закончилась|Открываем [вьюер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer?key=https%3A%2F%2Fyandex.ru&keyType=url), вводим урл главной страницы сайта и нажимаем кнопку **URL**. Ищем поле **BannerLandSampleCheckState**, которое содержит: время начала/окончания проверки семпла, HTTP коды скачивания урлов семпла. Если поля **BannerLandSampleCheckState**, значит, запрос не приходил.

{% endcut %}


## Скачивание урлов семпла для превью Смарта по сайту

Во время обработки запроса **datacamp-bannerland-host-check-ext** каждый урл семпла прокачивается с помощью заданий **check-url-for-smart-preview**. Урлы конкретных офферов можно взять из поля **BannerLandSampleCheckState**: открываем [](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer вьювер) , вводим урл [](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer?key=https%3A%2F%2Fliski.top4dom.ru%2F&keyType=url главной страницы), нажимаем кнопку **URL** и ищем поле **BannerLandSampleCheckState**. Если поля нет, значит запрос **datacamp-bannerland-host-check-ext** не приходил.


{% cut "В следующих местах могут быть проблемы с прокачкой конкретных урлов офферов. Пункты указаны в порядке, который следует использовать при отладке проблем" %}

Как изучать | Колонка по центру
:--- | :---
Задание не пришло| Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим урл оффера и нажимаем кнопку **URL**. Ищем поле **FeedsState**, а в нем секцию **check-url-for-smart-preview**. Если ее нет, то нужно смотреть последний пункт **Проверка семпла не стартовала, или стартовала, но не закончилась** из таблицы выше.
В задании нет DCMP контекста|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим урл оффера и нажимаем кнопку **URL**. Ищем поле **FeedsState**, а в нем секцию **check-url-for-smart-preview**., а в ней поле **FeedContext**. Если его нет, или оно пустое, то запрос пришел без контекста.
Урл оказался зафильтрован|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим урл оффера и нажимаем кнопку **URL**. Ищем поле **FilterState**. Если поле непустое, то урл зафильтрован и не будет качаться. В этом случае причина лежит в самом поле.
Урл не скачался|Открываем [вьюер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer?key=https%3A%2F%2Fyandex.ru&keyType=url), вводим урл главной страницы сайта и нажимаем кнопку **URL**. Ищем поле **BannerLandSampleCheckState**, а в нем нужный урл. Если у урла нет **HttpCode**, или он равен 0, то урл не скачался.
Урл не пришел из RTHUB в DCMP|Проверяем урл через [YQL-запрос](https://yql.yandex-team.ru/Operations/YkfiU7q3k8maPaXlLXY9KQHzsnXbOqhnBjGXyIoH1DM=). Смотрим на результаты и на время скачивания.
Урл не пришел из DCMP|Проверяем ссылку [YQL-запросом](https://yql.yandex-team.ru/Operations/YkbxkVZ1OzYVH07MCygGRMxxXCJ9EZCx2i6pGhQ5W-s=). Смотрим на результаты и на время обработки.

{% endcut %}

## Поурловая актуализация для превью Смарта по сайту

Директ сам поддерживает в актуальном состоянии набор офферов из превью по сайту. Для этого Директ посылает в Самовар запросы на скачивание офферов. Запрос на скачивание отправляется в Самовар через logbroker топик [samovar/feeds-ext](https://lb.yandex-team.ru/logbroker/accounts/samovar/feeds-ext?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&metricsFrom=1648710801568&metricsTo=1648797201569&sortOrder=%22default%22). Запрос должен отправляться на нужный урл, должен обозначаться строкой **datacamp-bannerland-offers-previews-ext** и должен содержать в себе [DCMP контекст](https://a.yandex-team.ru/arc_vcs/market/mbi/proto/SamovarContext.proto?rev=r9280743#L167). Более подробное описание по формированию запроса [находится тут](https://wiki.yandex-team.ru/robot/samovar/feedsext/).

{% cut "В следующих местах могут быть проблемы с прокачкой урлов офферов. Пункты указаны в порядке, который следует использовать при отладке проблем" %}

Как изучать | Колонка по центру
:--- | :---
Задание не пришло|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим урл и нажимаем кнопку **URL**. Смотрим поле **FeedsState**, ищем там секцию **datacamp-bannerland-offers-previews-ext**. Если секции **datacamp-bannerland-offers-previews-ext** нет, значит задание не пришло. Иначе в **LastSignal** будет время последнего задания. Так же можно грепнуть логи запросов Директа в Самовар https://yql.yandex-team.ru/Operations/YlCZT65ODx0MoBnRiXEGjjMmyT9OiTYh1Eas7zFEOz0=. В них DCMP контекст в читабельном виде.
В задании нет DCMP контекста|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим урл и нажимаем кнопку **URL**. Ищем поле **FeedsState**, в нем секцию **datacamp-bannerland-offers-previews-ext**, а в ней поле **FeedContext**. Если его нет, или оно пустое, то запрос пришел без контекста.
Урл оказался зафильтрован|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим урл и нажимаем кнопку **URL**. Смотрим поле **FilterState**. Если поле непустое, то урл зафильтрован и не будет качаться. Причина зафильтрованности лежит в самом поле **FilterState**.
Урл не запланировался|Открываем вьювер https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer, вводим урл и нажимаем кнопку **URL**. Ищем в поле **CrawlInfo** секцию с **DATACAMP_BANNERLAND_OFFERS**.
Урл не скачался|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим урл и нажимаем кнопку **URL**. Ищем поле **CrawlHistory**, а в нем секцию с консьюмером **DATACAMP_BANNERLAND_OFFERS**. Если ее нет, или дата скачивания старая, то урл не скачался. Так же можно грепнуть [логи планирования Самовара](https://yql.yandex-team.ru/Operations/YkfdStJwbJdTH1zAhRXFW_YnJVC9BAeqsFdH3yVnOag=) и [логи скачивания Зоры](https://yql.yandex-team.ru/Operations/YjsbYtJwbGhod4uOsq51-qC9nDQ8vRzYcN1EGPcxAJY=).
Урл не пришел из RTHUB в DCMP|Открываем YQL и [грепаем урл](https://yql.yandex-team.ru/Operations/YkfiU7q3k8maPaXlLXY9KQHzsnXbOqhnBjGXyIoH1DM=). Смотрим на результаты и на время скачивания.
Урл не пришел из DCMP|Открываем YQL и [грепаем урл](https://yql.yandex-team.ru/Operations/YkbxkVZ1OzYVH07MCygGRMxxXCJ9EZCx2i6pGhQ5W-s=). Смотрим на результаты и на время обработки.

{% endcut %}

## Скачивание урлов для Смарта по сайту

Самовар качает офферы для Смарта по сайту с помощью **пассивной** политики [datacamp-bannerland-offers](https://a.yandex-team.ru/arc/trunk/arcadia/robot/samovar/conf/conf-primary-arnold/crawl_config.pb.txt?rev=r9297073#L8193). Такая политика выбирает урлы из общего Самоварного потока скачивания. Сама она ничего не качает. Поэтому никаких гарантий, что урл прокачается за определенное время, нет.

{% cut "В следующих местах могут быть проблемы с прокачкой офферов сайта. Пункты указаны в порядке, которые следует использовать при отладке проблем" %}

Проблема | Что искать
:--- | :---
Хоста нет в MBI таблице [//home/market/production/mbi/samovar/sites-parsing/latest](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/mbi/samovar/sites-parsing/latest)|Проверяем [запросом в YQL](https://yql.yandex-team.ru/Operations/Yk0_A5fFt9VV_mPioDeVjXiz7I-6175ItOvu2ZyUI98=). Если хоста нет в таблице, то он либо не зарегистрирован в MBI, либо не пророс в таблицу. TODO: открываем YQL и грепаем логи MBI. Если хоста в логах регистрации нет, значит он не регистрировался.
Хост выключен в MBI|[Проверяем в YQL](https://yql.yandex-team.ru/Operations/Yk0_A5fFt9VV_mPioDeVjXiz7I-6175ItOvu2ZyUI98=). Смотрим на колонку **enabled**. Если значение **false**, то хост выключен.
Хост не включен в MBI|[Проверяем через YQL](https://yql.yandex-team.ru/Operations/Yk0_A5fFt9VV_mPioDeVjXiz7I-6175ItOvu2ZyUI98=). Смотрим на флаги **shopsDatParameters.direct_goods_ads**, **shopsDatParameters.direct_search_snippet_gallery**, **shopsDatParameters.direct_standby** в колонке **context-protobuf**. Если все флаги **false**, то хост не включен для Директа.
На хосте нет MBI контекста|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), в нем вводим хост и нажимаем кнопку **HOST**. Ищем поле **DataCampBannerlandOfferContext**. Если его нет, то контекст не доехал до Самовара из таблицы [//home/market/production/mbi/samovar/sites-parsing/latest](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/mbi/samovar/sites-parsing/latest). Контекст доезжает в среднем за 24 часа.
Хост зафильтрован|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим хост оффера и нажимаем кнопку **HOST**. Ищем поле **FilterState**. Если поле непустое, то хост зафильтрован и не будет качаться. В этом случае причина зафильтрованности лежит в самом поле.
Хост неглавное зеркало|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим хост оффера и нажимаем кнопку **HOST**. Ищем поле **MainMirror**. Если оно есть, то хост неглавное зеркало. Такие хосты не качаются Самоваром.
Урл зафильтрован|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим урл оффера и нажимаем кнопку **URL**. Ищем поле **FilterState**. Если поле непустое, то урл зафильтрован и не будет качаться. В этом случае причина зафильтрованности лежит в самом поле.
Самовар не качает урл|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим урл оффера и нажимаем кнопку **URL**. Ищем поле **CrawlHistory**. Смотрим последние скачивание с консьюмером **DATACAMP_BANNERLAND_OFFERS**.

{% endcut %}


## Прокачка редиректов
Для рекламы нужно иметь хост после редиректа, чтобы корректно работали фильтры по доменам на рекламных площадках

Для фидов Смартов и ДО происходит семплирование в DataCamp, 5 урлов для каждого исходного домена в фиде, не больше 10 доменов. Далее эти оферы отправляются в виде запросов из DC в Samovar через logbroker топик [samovar/feeds-ext](https://lb.yandex-team.ru/logbroker/accounts/samovar/feeds-ext?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&metricsFrom=1648710801568&metricsTo=1648797201569&sortOrder=%22default%22). Запрос должен отправляться на нужный урл, должен обозначаться строкой [datacamp-bannerland-offers-redirects](https://a.yandex-team.ru/arc/trunk/arcadia/robot/samovar/conf/conf-common/feeds_config.pb.txt?rev=r9254191#L876) и должен содержать в себе [DCMP контекст](https://a.yandex-team.ru/arc_vcs/market/mbi/proto/SamovarContext.proto?rev=r9280743#L167). В контексте **campaignType=REDIRECT directStandBy=true businessId, shopId**. Код отправки [здесь](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/controllers/lib/samovar_sender/samovar_sender.cpp?rev=r9283589#L44). Все эти офферы должны приоритетно прокачаться в Samovar политикой [datacamp-bannerland-offers-redirects](https://a.yandex-team.ru/arc/trunk/arcadia/robot/samovar/conf/conf-primary-arnold/crawl_config.pb.txt?rev=r9297073#L6899). Далее RTHUB отправляет обратно в DC редиректы - офферы, в которых проставлены:
1. **original_content->url** (урл после редиректов),
2. **original_url** (исходный),
3. **businessId, shopId** (бизнесшоп для которого прокачали редиректы),
4. **service->data_source=REDIRECT_RESOLVER** (маркер для DC что оффер не нужно сохранять в хранилище, а нужно сохранить редирект в таблицу партнеров)


{% note alert %}

{% cut "В следующих местах могут быть проблемы с прокачкой урлов офферов. Пункты указаны в порядке, который следует использовать при отладке проблем" %}

Проблема | Что искать
:--- | :---
Задание не пришло|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим урл и нажимаем кнопку **URL**. Смотрим поле **FeedsState**, ищем там секцию **datacamp-bannerland-offers-redirects**. Если секции **datacamp-bannerland-offers-redirects** нет, значит задание не пришло. Иначе в **LastSignal** будет время последнего задания. Так же можно запросить [логи запросов Директа в Самовар](https://yql.yandex-team.ru/Operations/YkfrYbq3k8maPbVypnAbgkme6-DSK0WL3rtoz16cQsM=).
В задании нет DCMP контекста|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим урл и нажимаем кнопку **URL**. Ищем поле **FeedsState**, в нем секцию **datacamp-bannerland-offers-previews-ext**, а в ней поле **FeedContext**. Если его нет, или оно пустое, то запрос пришел без контекста.
Урл оказался зафильтрован|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим урл и нажимаем кнопку **URL**. Смотрим поле **FilterState**. Если поле непустое, то урл зафильтрован и не будет качаться. Причина зафильтрованности лежит в самом поле **FilterState**.
Урл не запланировался|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим урл и нажимаем кнопку **URL**. Ищем в поле **CrawlInfo** секцию с **DATACAMP_BANNERLAND_OFFERS**.
Урл не скачался|Открываем [вьювер](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer), вводим урл и нажимаем кнопку **URL**. Ищем поле **CrawlHistory**, а в нем секцию с консьюмером **DATACAMP_BANNERLAND_OFFERS**. Если ее нет, или дата скачивания старая, то урл не скачался. Так же можно собрать [логи планирования Самовара](https://yql.yandex-team.ru/Operations/YkfdStJwbJdTH1zAhRXFW_YnJVC9BAeqsFdH3yVnOag=) и [логи скачивания Зоры](https://yql.yandex-team.ru/Operations/YjsbYtJwbGhod4uOsq51-qC9nDQ8vRzYcN1EGPcxAJY=).
Урл не пришел из RTHUB в DCMP|Открываем [YQL и ищем урл](https://yql.yandex-team.ru/Operations/YkfiU7q3k8maPaXlLXY9KQHzsnXbOqhnBjGXyIoH1DM=). Смотрим на результаты и на время скачивания.
Урл не пришел из DCMP|Открываем YQL и грепаем урл https://yql.yandex-team.ru/Operations/YkbxkVZ1OzYVH07MCygGRMxxXCJ9EZCx2i6pGhQ5W-s=. Смотрим на результаты и на время обработки.

{% endcut %}

{% endnote %}

## Документация

* [Документация по дебагу проблем от Владимира](https://wiki.yandex-team.ru/users/vlavrenchenko/diagnostika-prokachek-dikix-offerov-po-vjuveru-samovara/)
* [Отправка заданий на скачивание в Самовар](https://wiki.yandex-team.ru/robot/samovar/feedsext/)
* [Запись КМБ про Самовар+Директ](https://nda.ya.ru/t/A-n7lM734tKaWc)
* [Дельта для редактирования этой документации](https://delta.yandex-team.ru/page/epad/page/y8pm73d4wupz13fh)
