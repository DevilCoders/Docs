registry.yandex.net/partners/java/java-base - базовый образ с jdk для всех приложений, кроме hourglass
registry.yandex.net/partners/java/hourglass-base - базовый образ для hourglass, наследуется от java-base

При обновлении registry.yandex.net/partners/java/java-base:
1. Запушить новый образ в регистри
2. Поменять тег в Dockerfile на новый тег registry.yandex.net/partners/java/java-base
3. Поменять тег в hourglass/Dockerfile.base на новый тег registry.yandex.net/partners/java/java-base
4. Выполнить пункты из инструкции "При обновлении registry.yandex.net/partners/java/hourglass-base"
5. Если поменялась версия yandex-openjdk - то поменять ее в partner_ansible и в creator

При обновлении registry.yandex.net/partners/java/hourglass-base:
1. Запушить новый образ в регистри
2. Поменять тег в hourglass/Dockerfile на новый тег registry.yandex.net/partners/java/hourglass-base

Сборка registry.yandex.net/partners/java/java-base
```
export VERSION=1.00
docker build --file Dockerfile.base -t registry.yandex.net/partners/java/java-base:$VERSION .
docker push registry.yandex.net/partners/java/java-base:$VERSION
```

Сборка registry.yandex.net/partners/java/hourglass-base
```
export VERSION=1.00
docker build --file hourglass/Dockerfile.base -t registry.yandex.net/partners/java/hourglass-base:$VERSION .
docker push registry.yandex.net/partners/java/hourglass-base:$VERSION
```
