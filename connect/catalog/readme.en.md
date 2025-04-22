# Catalog

Yandex.Connect back office & tech support board<br>
[catalog.ws.yandex-team.ru](https://catalog.ws.yandex-team.ru)

**Dev prerequisites**: *NodeJS*, *Docker for Mac*, *git*, *[magicdev](https://github.yandex-team.ru/toolbox/magicdev)*

```sh
# setup
$ npm i

# to launch the app
$ npm run dev
# → https://localhost.msup.yandex-team.ru:8443/

# to fetch i18n updates from Tanker
$ npm run i18n

# to specify the app version in the current git branch, and
# to build and push a docker image of a specified version to Qloud
# after pushing changes to the repository
$ npm run push -- -v 0.0.0
```


## Live environments

**production**<br>
[catalog.ws.yandex-team.ru](https://catalog.ws.yandex-team.ru)<br>
[Directory production API](https://api-internal.directory.ws.yandex.net/docs/changelog.html) + production Directory database

**qa**<br>
[catalog-qa.ws.yandex-team.ru](https://catalog-qa.ws.yandex-team.ru)<br>
[Directory qa API](https://api-internal-qa.directory.ws.yandex.net/docs/changelog.html) + **production DB**

**test**<br>
[catalog-test.ws.yandex-team.ru](https://catalog-test.ws.yandex-team.ru)<br>
[Directory test API](https://api-internal-test.directory.ws.yandex.net/docs/changelog.html) + test DB

The levels of access to the specific functionality within Catalog are set via the [IDM](https://idm.yandex-team.ru/system/connect-admin) roles.

The [/test](https://catalog-test.ws.yandex-team.ru/test) playground for API tests is available for everyone in the `development` and `test` environments, and for users with the `admin` role in other environments.


## Deployment

[workspace/dashboard](https://qloud-ext.yandex-team.ru/projects/workspace/dashboard) @ Qloud


## Content & i18n

[Directory Dashboard](https://tanker.yandex-team.ru/?project=directory-dashboard&branch=master) @ Tanker



## TVM resources

[production client](https://abc.yandex-team.ru/services/WS/resources/?show-resource=3168808) id: 2000991<br>
[production server](https://abc.yandex-team.ru/services/WS/resources/?show-resource=3168782) id: 2000985

[test client](https://abc.yandex-team.ru/services/WS/resources/?show-resource=3168807) id: 2000989<br>
[test server](https://abc.yandex-team.ru/services/WS/resources/?show-resource=3168781) id: 2000983

*— [Details](https://st.yandex-team.ru/DIR-4487)*

## Issue tracker

[DIR](https://st.yandex-team.ru/createTicket?queue=DIR&tags=catalog) queue @ Tracker