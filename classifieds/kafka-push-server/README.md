kafka-push-server
================


An obsolete service to stream logs from other obsolete services to kafka-push-server instance's file system

The only module is kafka-push-server-worker

#### Build commands

The project is built using java 8. On macos you'd probably need to `export JAVA_HOME=(/usr/libexec/java_home -v 1.8)`

  * Build:

`mvn clean install --projects kafka-push-server-worker --also-make --batch-mode`

  * Deploy:

Deployed via a [teamcity build](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_KafkaPushServer_KafkaPushServerAutoreleaseArc?mode=builds)
