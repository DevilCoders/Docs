# raw-ubuntu
Базовые Docker-образы ubuntu для тулзовых проектов в Qloud. В ванильном образе ubuntu из DockerHub нет наших репозиториев, нет утилит нужных для администрирования и там не прописан mirror.yandex.ru в sources.list.

Для сборки достаточно клонировать этот репозиторий и выполнить одну из этих команд:

    make precise
    make trusty
    make xenial
    make bionic
    make focal
