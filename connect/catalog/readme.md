# Каталог

Каталог организаций в Директории, внутренняя админка Яндекс.Коннекта<br>
[catalog.ws.yandex-team.ru](https://catalog.ws.yandex-team.ru)

Необходимое для запуска на локальной машине:<br>
*NodeJS*, *Docker for Mac*, *git*, *[magicdev](https://github.yandex-team.ru/toolbox/magicdev)*

```sh
# приготовление
$ npm i

# запуск
$ npm run dev
# → https://localhost.msup.yandex-team.ru:8443/

# обновление локализации из Танкера
$ npm run i18n

# обновление версии в текущей git-ветке,
# сборка и заливка докер-образа заданной версии в Qloud
# после заливки изменений в репозиторий
$ npm run push -- -v 0.0.0
```


## Окружения

**production**<br>
[catalog.ws.yandex-team.ru](https://catalog.ws.yandex-team.ru)<br>
[production-API Директории](https://api-internal.directory.ws.yandex.net/docs/changelog.html) + production-база данных Директории

**qa**<br>
[catalog-qa.ws.yandex-team.ru](https://catalog-qa.ws.yandex-team.ru)<br>
[qa-API Директории](https://api-internal-qa.directory.ws.yandex.net/docs/changelog.html) + **production-БД**

**test**<br>
[catalog-test.ws.yandex-team.ru](https://catalog-test.ws.yandex-team.ru)<br>
[test-API Директории](https://api-internal-test.directory.ws.yandex.net/docs/changelog.html) + test-БД

Уровни доступа к функционалу внутри Каталога определяются [IDM](https://idm.yandex-team.ru/system/connect-admin)-ролями.

Площадка [/test](https://catalog-test.ws.yandex-team.ru/test) для тестирования API доступна для всех в окружениях `development` и `test` и для пользователей с ролью `admin` в остальных окружениях.


## Развёртывание

#### [Y.Deploy](https://deploy.yandex-team.ru/projects/connect)
* Статичные дев-стенды: [stand1](https://deploy.yandex-team.ru/stages/tools_connect-catalog_testing_stand1) | [stand2](https://deploy.yandex-team.ru/stages/tools_connect-catalog_testing_stand2)
* [testing](https://deploy.yandex-team.ru/stages/tools_connect-catalog_testing)
* [integration-qa](https://deploy.yandex-team.ru/stages/tools_connect-catalog_integration-qa)
* [qa](https://deploy.yandex-team.ru/stages/tools_connect-catalog_qa)
* [production](https://deploy.yandex-team.ru/stages/tools_connect-catalog_production)

Переопределить бэкенд Директории через переменную окружения: `CATALOG_API__DIRECTORY=https://dir-9721.directory.test.ws.yandex.net`

#### Awacs
* testing и preprod – общие неймспейсы для Каталога и Коннекта
* [testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/connect_www_testing/show/)
* [preprod](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/connect_www_preprod/show/) (qa и integration-qa)
* [production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/connect_www_production/show/)

#### RPS лимитирование
 * [конфиг рейтлимитера](https://rpslimiter.z.yandex-team.ru/records/main/catalog360/editor)
 * [графики срабатывания лимитов](https://monitoring.yandex-team.ru/projects/catalog360/dashboards/mon3d4bgeecan04grjue)


## Контент и локализация

[Directory Dashboard](https://tanker-beta.yandex-team.ru/project/directory-dashboard) в новом Танкере

## TVM-ресурсы

id [production-клиента](https://abc.yandex-team.ru/services/WS/resources/?show-resource=3168808): 2000991<br>
id [production-сервера](https://abc.yandex-team.ru/services/WS/resources/?show-resource=3168782): 2000985

id [test-клиента](https://abc.yandex-team.ru/services/WS/resources/?show-resource=3168807): 2000989<br>
id [test-сервера](https://abc.yandex-team.ru/services/WS/resources/?show-resource=3168781): 2000983

*— [Подробнее](https://st.yandex-team.ru/DIR-4487)*

## Трекер

Очередь [DIR](https://st.yandex-team.ru/createTicket?queue=DIR&tags=catalog)
