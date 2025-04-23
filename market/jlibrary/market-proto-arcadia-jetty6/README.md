Java библиотека с транзиктивной зависимостью на прото файлы маркета. Нужна для использования протобафов в гитхабе

Локальная Сборка
------
В локальный Maven репозитарий библиотеку можно собрать выполнив:
```
ya make -DJDK_VERSION=8 --maven-export --deploy --sources --repository-id=maven-local --repository-url="file:///home/{USER}/.m2/repository"
```

Релиз
-----
Чтобы обновить библиотеку в артифактори, надо зайти в [релизную машину](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/market-proto-library-jetty6),
вставить необходимую ревизию и создать релиз по-последнему коммиту из аркадии (троеточие напротив коммита).
После отработки пайплайна библиотека с новой версией ляжет в [артифактори](http://artifactory.yandex.net/webapp/#/artifacts/browse/tree/General/yandex_market_releases/ru/yandex/market-proto-arcadia-jetty6).

