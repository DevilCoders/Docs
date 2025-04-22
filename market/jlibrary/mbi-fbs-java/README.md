Немного History
------
Чтобы постоянно не копировать изменения из аркадии в гитхаб, было принято решение сделать отдельную сборку прото-файлов 
с помощью [релизной машины](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/mbi-fbs) 
с [пайплайном](https://tsum.yandex-team.ru/pipe/projects/jlibrary/pipelines/mbi-fbs) 
которая кладёт библиотечку в [артифактори](http://artifactory.yandex.net/artifactory/yandex_market_releases/ru/yandex/market/mbi-fbs-java/)

Локальная Сборка
------
В локальный Maven репозитарий библиотеку можно собрать выполнив:
```
ya make -DJDK_VERSION=8 --maven-export --deploy --sources --repository-id=maven-local --repository-url="file:///home/{USER}/.m2/repository"
```
