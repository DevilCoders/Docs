Java библиотека с транзиктивной зависимостью на прото файлы оферного хранилища (датакемпа)

Немного History
------
Чтобы постоянно не копировать изменения из аркадии в гитхаб, было принято решение сделать отдельную сборку датакемповских прото-файлов 
с помощью [релизной машины](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/datacamp-proto-java-library) с [пайплайном](https://tsum.yandex-team.ru/pipe/projects/jlibrary/pipelines/datacamp-proto-java-library) 
которая кладёт библиотечку в [артифактори](http://artifactory.yandex.net/webapp/#/artifacts/browse/tree/General/yandex_market_releases/ru/yandex/idx-datacamp-proto)

Локальная Сборка
------
В локальный Maven репозитарий библиотеку можно собрать выполнив:
```
ya make -DJDK_VERSION=8 --maven-export --deploy --sources --repository-id=maven-local --repository-url="file:///home/{USER}/.m2/repository"
```

Релиз
-----
Чтобы обновить библиотеку в артифактори, надо зайти в [релизную машину](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/datacamp-proto-java-library), 
вставить необходимую ревизию из https://a.yandex-team.ru/arc/history/trunk/arcadia/market/idx/datacamp/proto и создать релиз по-последнему коммиту из аркадии (троеточие напротив коммита).
После отработки пайплайна библиотека с новой версией ляжет в [артифактори](http://artifactory.yandex.net/webapp/#/artifacts/browse/tree/General/yandex_market_releases/ru/yandex/idx-datacamp-proto).
Так же обновятся библиотеки [market-proto-common](http://artifactory.yandex.net/webapp/#/artifacts/browse/tree/General/yandex_market_releases/ru/yandex/market-proto-common) и [market-proto-ir](http://artifactory.yandex.net/webapp/#/artifacts/browse/tree/General/yandex_market_releases/ru/yandex/market-proto-ir)

Зависимости на которые опирается датакепм в проекте заводятся как:
- `ru.yandex:idx-datacamp-proto`
- `ru.yandex:market-proto-common`
- `ru.yandex:market-proto-ir`
