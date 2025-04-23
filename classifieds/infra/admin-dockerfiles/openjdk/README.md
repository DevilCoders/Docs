# [Zulu Community OpenJDK](https://www.azul.com/downloads/zulu-community/)

 ```docker
 // JRE ~300 mb
 FROM registry.yandex.net/vertis/openjdk:jre8
 FROM registry.yandex.net/vertis/openjdk:jre11
 FROM registry.yandex.net/vertis/openjdk:jre14
 FROM registry.yandex.net/vertis/openjdk:jre15
 FROM registry.yandex.net/vertis/openjdk:jre16
 FROM registry.yandex.net/vertis/openjdk:jre17

 // JDK ~500 mb
 FROM registry.yandex.net/vertis/openjdk:jdk8
 FROM registry.yandex.net/vertis/openjdk:jdk11
 FROM registry.yandex.net/vertis/openjdk:jdk14
 FROM registry.yandex.net/vertis/openjdk:jdk15
 FROM registry.yandex.net/vertis/openjdk:jdk16
 FROM registry.yandex.net/vertis/openjdk:jdk17
 ```

Образ с сертифицированной сборкой OpenJDK от [Azul](https://www.azul.com/).

Образ [**автоматически**](https://t.vertis.yandex-team.ru/project/VerticalsBackend_DockerOpenjdk?mode=builds) обновляется со свежей `tzdata` и внутренними сертификатами.
Не забывайте делать `--pull`!

Для сервисов, которым нужна впаяная geodata, есть образы с суффиксом `-geobase6`.
