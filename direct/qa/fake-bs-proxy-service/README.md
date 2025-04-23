# fake-bs-proxy-service

Service for log requests from Direct to BS.
Also it generates default responses.

TODO: proxy request to BS, with possibility to modify/override requests and/or responses 
Todo: ПИСАТЬ ЛОГИ

# Локальный запуск и использование
счекаутить репозиторий, создать проект из корневого pom, добавить модулями вложенные.

`mvn clean package` из корня

запустить **JettyDebugStarter**

прокинуть порты на ppcdev: `ssh -R127.0.0.5:YOUR_FREE_BETA_PORT:127.0.0.1:9010 -AN ppcdevN.yandex.ru`

поменять в тестах свойство **direct.transport.fake.bs.host** на `http://YOUR_FREE_BETA_PORT.betaN.direct.yandex.ru/proxy/`

# Сборка руками
1. `git clone https://github.yandex-team.ru/direct-qa/jetty-starter`
1. `cd jetty-starter && mvn clean package && cd ..`
1. `svn co svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/direct/qa/fake-bs-proxy-service`
1. `cd fake-bs-proxy-service`
1. `mvn clean package`
1. `cp ../jetty-starter/target/jetty-starter-1.0-SNAPSHOT-jar-with-dependencies.jar ./jetty-starter.jar`
1. `docker build -t registry.yandex.net/direct-qa/applications:fake-bs-proxy-<ДАТА> .`
(в IDM должна быть роль contributor на докерный репозиторий direct-qa)
1. `docker push registry.yandex.net/direct-qa/applications:fake-bs-proxy-<ДАТА>`
1. `rm jetty-starter.jar`

# Сборка силами Jenkins
Вроде бы удалось добиться корректной сборки на Jenkins. Для этого нужно вручную запустить задачу https://jenkins-new.qart.yandex-team.ru/job/direct-applications/job/fake-bs-proxy/ c тегом в виде текущей даты

# Обновление и деплой
обновить в deploy инстанс https://deploy.yandex-team.ru/stage/direct-bs-test-proxy по инструкции https://docs.yandex-team.ru/direct-dev/guide/jeri/ts-ext-tools-update
