### Датакемповые зависимости переехали в `artifactory.yandex.net`

Сейчас датакемповские прото-файлы лежат в [аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/market/datacamp/proto).
Чтобы постоянно не копировать изменения из аркадии в гитхаб, было принято решение сделать отдельную сборку [библиотеки](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/datacamp-proto) 
которая с помощью [релизной машины](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/datacamp-proto-java-library) с [пайплайном](https://tsum.yandex-team.ru/pipe/projects/jlibrary/pipelines/datacamp-proto-java-library) 
выкладывается в [артифактори](http://artifactory.yandex.net/webapp/#/artifacts/browse/tree/General/yandex_market_releases/ru/yandex/idx-datacamp-proto)

Чтобы обновить библиотеку в артифактори, надо зайти в [релизную машину](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/datacamp-proto-java-library), 
вставить необходимую ревизию из https://a.yandex-team.ru/arc/history/trunk/arcadia/market/idx/datacamp/proto и создать релиз по-последнему коммиту из аркадии (троеточие напротив коммита).
После отработки пайплайна библиотека с новой версией ляжет в [артифактори](http://artifactory.yandex.net/webapp/#/artifacts/browse/tree/General/yandex_market_releases/ru/yandex/idx-datacamp-proto).
Так же обновятся библиотеки [market-proto-common](http://artifactory.yandex.net/webapp/#/artifacts/browse/tree/General/yandex_market_releases/ru/yandex/market-proto-common) и [market-proto-ir](http://artifactory.yandex.net/webapp/#/artifacts/browse/tree/General/yandex_market_releases/ru/yandex/market-proto-ir)

Зависимости на которые опирается датакепм в проекте заводятся как:
`ru.yandex:idx-datacamp-proto`
`ru.yandex:market-proto-common`
`ru.yandex:market-proto-ir`
