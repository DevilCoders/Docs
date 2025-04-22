Java библиотека с транзиктивной зависимостью на прото файлы интеграции MDM <-> IRIS

Сборка
------
В локальный Maven репозитарий библиотеку можно собрать выполнив:
```
ya make -DJDK_VERSION=8 --maven-export --deploy --sources --repository-id=maven-local --repository-url="file:///home/{USER}/.m2/repository"
```

Релиз
-----
Публикация либы производится после коммита в trunk через 
[релизную машину](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/mdm-proto).
