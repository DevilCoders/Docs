### ya.make PEERDIR structure
```
PEERDIR(
    [external libraries (/contrib)]

    [yandex common libraries (/library)]

    [yandex non-crm project libraries]

    [crm libraries (/crm)]
)
```

{% cut "Example" %}
```
PEERDIR(
    contrib/java/com/typesafe/config
    contrib/java/io/insert-koin/koin-core-jvm
    contrib/java/io/github/microutils/kotlin-logging-jvm
    contrib/java/org/hibernate/hibernate-core

    library/java/tvmauth

    apphost/api/service/java/apphost
    apphost/proto/extensions

    crm/apphost/proto
    crm/library/kotlin/service
)
```
{% endcut %}
