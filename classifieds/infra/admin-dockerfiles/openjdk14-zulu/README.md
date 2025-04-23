# [Zulu Community OpenJDK 14](https://www.azul.com/downloads/zulu-community/?version=java-14&os=linux&architecture=x86-64-bit&package=jdk)

 ```FROM registry.yandex.net/vertis/openjdk14-zulu:latest```

Образ с сертифицированной сборкой OpenJDK 14 от [Azul](https://www.azul.com/).

Образ **автоматически** [`ONBUILD`](https://docs.docker.com/engine/reference/builder/#onbuild) обновляет `tzdata` и `YandexInternalRootCA` при каждой сборке дочерних контейнеров до актуальной версии.

Дополнительно при необходимости можно вызвать утилиту `jre-cert-update` и добавить любой другой сертификат, просто добавьте в свой `Dockerfile` это:

```RUN jre-cert-update <алиас для сертификата> <URL откуда взять сертификат>```
