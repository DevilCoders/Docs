### Проекты группы taxifrontend

**Сборки**

| Service | Last pre-release | Last unstable |
| :-------------- | :--------------: | ------------: |
| Yandex | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_FrontendMonorepo_Stable,branch:taxifrontend-taxi-frontend-yandex/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_FrontendMonorepo_Stable&branch=taxi-frontend-yandex) | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_Infranaim_Frontend_NewFlowTest,branch:taxifrontend-taxi-frontend-yandex/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_Infranaim_Frontend_NewFlowTest&branch=taxi-frontend-yandex) |
| Uber | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_FrontendMonorepo_Stable,branch:taxifrontend-taxi-frontend-uber/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_FrontendMonorepo_Stable&branch=taxi-frontend-uber) | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_Infranaim_Frontend_NewFlowTest,branch:taxifrontend-taxi-frontend-uber/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_Infranaim_Frontend_NewFlowTest&branch=taxi-frontend-uber) |
| Yango | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_FrontendMonorepo_Stable,branch:taxifrontend-taxi-frontend-yango/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_FrontendMonorepo_Stable&branch=taxi-frontend-yango) | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_Infranaim_Frontend_NewFlowTest,branch:taxifrontend-taxi-frontend-yango/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_Infranaim_Frontend_NewFlowTest&branch=taxi-frontend-yango) |
| Go | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_FrontendMonorepo_Stable,branch:taxifrontend-taxi-frontend-go/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_FrontendMonorepo_Stable&branch=taxi-frontend-go) | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_Infranaim_Frontend_NewFlowTest,branch:taxifrontend-taxi-frontend-go/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_Infranaim_Frontend_NewFlowTest&branch=taxi-frontend-go) |
| Vezet | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_FrontendMonorepo_Stable,branch:taxifrontend-frontend-vezet/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_FrontendMonorepo_Stable&branch=frontend-vezet) | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_Infranaim_Frontend_NewFlowTest,branch:taxifrontend-frontend-vezet/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_Infranaim_Frontend_NewFlowTest&branch=frontend-vezet) |

**Error logs**

| Service | stable | testing | unstable | client |
| :-------------- | --------------: | --------------: | ------------: | ------------: |
| Yandex | [stable](https://kibana.taxi.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-taxi-frontend-yandex'),sort:!(!('@timestamp',desc)))) | [testing](https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-taxi-frontend-yandex'),sort:!(!('@timestamp',desc)))) | [unstable](https://kibana.taxi.dev.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-taxi-frontend-yandex'),sort:!(!('@timestamp',desc)))) | [тут](https://error.yandex-team.ru/projects/taxi-frontend.yandex/projectDashboard) |
| Uber | [stable](https://kibana.taxi.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-taxi-frontend-uber'),sort:!(!('@timestamp',desc)))) | [testing](https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-taxi-frontend-uber'),sort:!(!('@timestamp',desc)))) | [unstable](https://kibana.taxi.dev.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-taxi-frontend-uber'),sort:!(!('@timestamp',desc)))) | [тут](https://error.yandex-team.ru/projects/taxi-frontend.uber/projectDashboard) |
| Yango | [stable](https://kibana.taxi.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-taxi-frontend-yango'),sort:!(!('@timestamp',desc)))) | [testing](https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-taxi-frontend-yango'),sort:!(!('@timestamp',desc)))) | [unstable](https://kibana.taxi.dev.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-taxi-frontend-yango'),sort:!(!('@timestamp',desc)))) | [тут](https://error.yandex-team.ru/projects/taxi-frontend.yango/projectDashboard) |
| Go | [stable](https://kibana.taxi.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-taxi-frontend-go'),sort:!(!('@timestamp',desc)))) | [testing](https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-taxi-frontend-go'),sort:!(!('@timestamp',desc)))) | [unstable](https://kibana.taxi.dev.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-taxi-frontend-go'),sort:!(!('@timestamp',desc)))) | [тут](https://error.yandex-team.ru/projects/taxi-frontend.go/projectDashboard) |
| Vezet | [stable](https://kibana.taxi.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-frontend-vezet'),sort:!(!('@timestamp',desc)))) | [testing](https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-frontend-vezet'),sort:!(!('@timestamp',desc)))) | [unstable](https://kibana.taxi.dev.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxifrontend-frontend-vezet'),sort:!(!('@timestamp',desc)))) | [тут](https://error.yandex-team.ru/projects/taxi-frontend.vezet/projectDashboard) |

[daily uptime dashboard](https://monitoring.yandex-team.ru/projects/taxi/dashboards/monmf8u65r9be8gckukj?range=1d&refresh=60)

**env**

| Service | stable | testing | unstable |
| :-------------- | :-------------- | :-------------- | ------------: |
| Yandex | [taxi.yandex.ru](https://taxi.yandex.ru) | [rtc balancer](https://taxi-frontend-yandex.taxi.tst.yandex.net)<br/>[public dns](https://taxi-frontend.taxi.tst.yandex.ru) | [rtc balancer](https://taxi-frontend-yandex.taxi.dev.yandex.net)<br/>[public dns](https://taxi-frontend.taxi.dev.yandex.ru) |
| Uber | [support-uber.com](https://support-uber.com) | [rtc balancer](https://taxi-frontend-uber.taxi.tst.yandex.net)<br/>[public dns](https://taxi-uber-frontend-uber.taxi.tst.yandex.com) | [rtc balancer](https://taxi-frontend-uber.taxi.dev.yandex.net)<br/>[public dns](https://taxi-uber-frontend-uber.taxi.dev.yandex.com) |
| Yango | [yango.yandex.com](https://yango.yandex.com) | [rtc balancer](https://taxi-frontend-yango.taxi.tst.yandex.net)<br/>[public dns](https://yango-frontend-uber.taxi.tst.yandex.net) | [rtc balancer](https://taxi-frontend-yango.taxi.dev.yandex.net)<br/>[public dns](https://yango-frontend-uber.taxi.dev.yandex.net) |
| Go | [go.yandex](https://go.yandex) | [rtc balancer](https://taxi-frontend-go.taxi.tst.yandex.net)<br/>[public dns](https://go.taxi.tst.yandex.net) | [rtc balancer](https://taxi-frontend-go.taxi.dev.yandex.net)<br/>[public dns](https://go.taxi.dev.yandex.net) |
| Vezet | [tariff.vezet.ru](https://tariff.vezet.ru) | [rtc balancer](https://frontend-vezet.taxi.tst.yandex.net) | - |

## разработка

**Сервис разрабатывается на дев машинках [QYP](https://wiki.yandex-team.ru/taxi/web/yp-frontend-guide/)**

Маутим [аркадию](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#system-requirements) в ~ на машинке. Должен получиться путь `~/arc/arcadia/taxi/frontend`. Если у вас проект лежит в другой папке - порпавьте файлы nginx сервиса

**Важно:** Маутнить аркадию надо с флагом --allow-other, но для его спервать дать права на fuse конфиг

```(bash)
addgroup <username> fuse
arc mount --allow-other -m arcadia/ -S store/
```

**Use NodeJs version 12**

Установка зависимостей

> Если у вас **mac**, вам нужно поставить `coreutils` из `brew`, чтобы корректно создались симлинки

```bash
npm ci
cd projects/<service>/
npm ci
```

Запуск проекта в development режиме:

```bash
npm run run {service}
```

Для сборки отдельных entry point'ов:

```bash
npm run run {service} -- --entry=app/index
npm run run {service} -- --entry=app/index,webview/help
npm run run {service} -- --entry=webview
```

Так же необходимо положить [эти файлы из секретницы](https://yav.yandex-team.ru/secret/sec-01em1n08qkksbybh8rmwxbv30a/explore/versions) в домик `~`:
1. Качаем архив последней версии
2. Распаковываем (внутри лежат файлы вида `.tvm-{service}.json`)
3. Копируем их на дев машинку. Например `scp .tvm-yandex.json {USER_NAME}@{USER_NAME}.sas.yp-c.yandex.net:~`

Так же необходимо скопировать nginx конфиги в /etc/nginx и рестартануть nginx `sudo service nginx restart`
```bash
npm run sync:nginx -- {service}
```
Скрипт разложит дев конфиги nginx сервиса в нужные места (/etc/nginx/)

#### SSR

Чтобы запустить приложение с серверным рендерингом нужно:
1. Выключить `hotRender` в `projects/common/server/configs/development.js`

```diff
{
  app: {
-    hotRender: true,
+    hotRender: false
  },
  …
}
```

2. Собрать в development/production mode

```bash
npm run build # or npm run build:prod
```

3. Запустить в development/production mode

```bash
npm run run # or npm run start
```

#### Тесты

```bash
npm run test:dev
```

Тесты размещаем в папке `__tests__` рядом с тестируемыми компонентами.

[Настройка IDE Webstorm](https://medium.com/front-end-hacking/fix-element-is-not-imported-jest-describe-it-expect-in-webstorm-aaf8c29ae3c2)

#### Возможные проблемы
1. При запуске билд упал с ошибок и повторный запуск ругается на ` tvmtool: Error: failed to use port (main interface) 8001: listen tcp 127.0.0.1:8001: bind: address already in use`

*Вероятнее всего проблема в подвишем tmv демоне*.
`ps aux | grep tvmtool` далее убиваем процессы которые смотрят на ваш tvm токен `kill -9 {process_id}`

#### Как добавить язык в хэлп таксоментра
На примере норвежского языка в Норвегии

1. добавляем в availableLanguagesByCountries для страны норвегия (NO) список всех доступных в данной стране языков, считаем что во всех странах международки доступны все языки международки. таким образом
добавляем { NO: INTERNATIONAL_AVAILABLE_LANGUAGES }

2. при этом необходимо добавить норвежский язык (no) в список допустимых INTERNATIONAL_AVAILABLE_LANGUAGES = ['no']

3. Добавляем норвежский также в allAvailableLanguages

4. И если есть необходимость в маппиге кодов языков добавляем в langdetect.mapping

5. А также проверяем и добавляем необходимый маппинг в momentLanguages

6. Если язык right-to-left, то добавляем его rtlLanguages
