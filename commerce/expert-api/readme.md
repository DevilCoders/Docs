# expert-api [![Build Status](https://drone.yandex-team.ru/api/badges/expert/expert-api/status.svg)](https://drone.yandex-team.ru/expert/expert-api)

Новый backend для Эксперта.
Технологии:

 * __nodejs__ `10`
 * __postgres__

## [Документация репозитория](https://wiki.yandex-team.ru/bliss/expert/api/)

## [Документация API](https://github.yandex-team.ru/pages/expert/expert-api-docs/v1/)

## Доступы

**Продакшн** — `_EXPERTNETS_`

Direct: [intapi.direct.yandex.ru](https://golem.yandex-team.ru/hostinfo.sbml?object=intapi.direct.yandex.ru)

MDS write: [storage-int.mds.yandex.net](https://golem.yandex-team.ru/hostinfo.sbml?object=storage-int.mds.yandex.net):1111

MDS read: [storage.mds.yandex.net](https://golem.yandex-team.ru/hostinfo.sbml?object=storage.mds.yandex.net):80

Avatars write: [avatars-int.mds.yandex.net](https://golem.yandex-team.ru/hostinfo.sbml?object=avatars-int.mds.yandex.net):13000

**Тестинг** — `_EXPERTTESTNETS_`

Direct: [ppctest-ts1-front.yandex.ru](https://golem.yandex-team.ru/hostinfo.sbml?object=ppctest-ts1-front.yandex.ru):9000

MDS write: [storage-int.mdst.yandex.net](https://golem.yandex-team.ru/hostinfo.sbml?object=storage-int.mdst.yandex.net):1111

MDS read: [storage.mdst.yandex.net](https://golem.yandex-team.ru/hostinfo.sbml?object=storage.mdst.yandex.net):80

Avatars write: [avatars-int.mdst.yandex.net](https://golem.yandex-team.ru/hostinfo.sbml?object=avatars-int.mdst.yandex.net):13000

## Создание тестовых сертификатов по каждому тесту

Перейти в /app и выполнить команду `NODE_PATH=. node ./scripts/createTestCertificates.js`

## Создание тестовых сертификатов для Директа

Перейти в /app и выполнить команду `NODE_PATH=. node ./scripts/createDirectCertificates.js`

## Настройка мониторингов qloud и mdb

1. [Получаем токены](https://github.yandex-team.ru/toolbox/monitorado#%D0%A2%D0%BE%D0%BA%D0%B5%D0%BD%D1%8B) и кладем в `.env`

1. Меняем по необходимости `.monitorado.yml`

1. Смотрим, что изменилось:

        npx monitorado diff -v

1. Проливаем:

        npx monitorado exec -v
