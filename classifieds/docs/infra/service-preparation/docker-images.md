# Docker images/docker registry
## Основное
Считаем основным хранилищем для тегов и образов докер контейнеров: registry.yandex.net . Это значит, что все наши образы и теги должны храниться в нём.
Документация тут: [https://wiki.yandex-team.ru/docker-registry/](https://wiki.yandex-team.ru/docker-registry/)

Особенности, про которые надо знать:
1. Базовые образы ubuntu хранятся в префиксе vertis-base/ . В докерфайлах используем:
  `FROM registry.yandex.net/vertis-base/ubuntu:trusty`
либо:
  `FROM registry.yandex.net/vertis-base/ubuntu:xenial`
либо:
  `FROM registry.yandex.net/vertis-base/ubuntu:bionic`

Отличия наших базовых образов от базовых образов убунты:
- подключены apt репозитории Вертикалей
- добавлен в доверенные центры сертификации наш внутренний CA
- докерфайлы тут: [xenial](https://a.yandex-team.ru/arcadia/classifieds/infra/admin-dockerfiles/ubuntu-base/xenial.Dockerfile), [focal](https://a.yandex-team.ru/arcadia/classifieds/infra/admin-dockerfiles/ubuntu-base/focal.Dockerfile)

2. Cобранные docker образы заливаем в `registry.yandex.net/vertis/<имя_образа>:<тег>`
3. Все сотрудники Вертикалей имеют доступы на чтение из `registry.yandex.net/vertis-base/` и на чтение/запись в `registry.yandex.net/vertis/` . Подробнее про авторизацию [тут](https://wiki.yandex-team.ru/docker-registry/#authorization).
4. Авторизация на teamcity агентах и github раннерах уже настроена.

## Про деплой
На наших серверах поднят кэширующий registry proxy ( [адрес](https://registry-proxy-int.noc-slb.prod.vertis.yandex.net/). Во время деплоя (дабы снизить нагрузку на registry.yandex.net ), адрес `registry.yandex.net`  автоматом меняется на `registry-proxy-int.noc-slb.prod.vertis.yandex.net`
Если нужный образ есть в кэше - он берется из него, если образ в кэше отсутствует - он скачивается с `registry.yandex.net` и кладётся в кэш.

## FAQ
1. Как c помощью curl проверить наличие тега в registry.yandex.net
`curl --insecure -s -H 'Authorization: Basic <TOKEN>' https://registry.yandex.net/v2/vertis/<image_name>/manifests/<tag>`
2. Где взять для basic auth?
Подсмотреть в файле `~/.docker/config.json`, либо получить командой: `echo -n '<ваш_логин>:<OAuth_Token>' | base64`

