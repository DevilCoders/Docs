Java библиотека с транзитивной зависимостью на прото файлы Самовара

Локальная Сборка
------
В локальный Maven репозитарий библиотеку можно собрать выполнив:
```
ya make -DJDK_VERSION=8 --maven-export --deploy --sources --repository-id=maven-local --repository-url="file://${HOME}/.m2/repository"
```

