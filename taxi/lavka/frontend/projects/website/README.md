# Lavka web

Веб-версия Яндекс.Лавки<br/>
Документация по разработке на [Вики](https://wiki.yandex-team.ru/lavka/web/)

---

## Documentation

- [CONTRIBUTING](docs/CONTRIBUTING.md)
- [Styleguide](docs/styleguide.md)
- [Как писать a11y код](docs/a11y.md)
- [Переводы](https://a.yandex-team.ru/arc_vcs/taxi/lavka/frontend/packages/i18n/README.md)
- [Нагрузочное тестирование](.load-testing/README.md)
- [Релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/release/)

---

## Ссылки

### Общие
- [Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/35/edit/354720/info)
- [Figma](https://www.figma.com/file/PJG55GXBl8cYdcN2AnFMnF/Десктоп?node-id=1568%3A202)
- [GAP Config](https://tariff-editor.taxi.yandex-team.ru/authproxies/grocery-authproxy/show/LzQuMC9ncm9jZXJ5LXN1cGVyYXBwL2xhdmth)

### По окружению
| Service | Production                                   | Testing                                           |
|---------|----------------------------------------------|---------------------------------------------------|
| CSP     | https://csp.yandex-team.ru/projects/lavkaweb | https://csp.yandex-team.ru/projects/lavkaweb_test |

---

## Experiments and Configs

| Environment | Experiments                                                                                                                                       | Configs                                                                                                                                       |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| testing     | [Link](https://tariff-editor.taxi.tst.yandex-team.ru/experiments3/experiments?enabled=all&active=all&order=name_desc&name=lavka-frontend_desktop) | [Link](https://tariff-editor.taxi.tst.yandex-team.ru/experiments3/configs?enabled=all&active=all&order=name_desc&name=lavka-frontend_desktop) |
| production  | [Link](https://tariff-editor.taxi.yandex-team.ru/experiments3/experiments?active=all&enabled=all&name=lavka-frontend_desktop)                     | [Link](https://tariff-editor.taxi.yandex-team.ru/experiments3/configs?active=all&enabled=all&name=lavka-frontend_desktop)                     |

### Локальные эксперименты

Для удобства разработки можно задавать необходимые конфиги и эксперименты внутри `.dev/local/`

### Особые эксперименты и конфиги

- [Специальные лавки](https://tariff-editor.taxi.yandex-team.ru/experiments3/configs/show/overlord_depots_hidings/current?active=all&enabled=all&name=overlord_depots_hidings)
- [Зоны](https://tariff-editor.taxi.yandex-team.ru/experiments3/experiments/show/grocery_geo_onboarding/current?enabled=all&active=all&name=grocery_geo_onboarding)
- [Кешбек](https://tariff-editor.taxi.yandex-team.ru/experiments3/experiments/show/grocery_cashback/current?active=all&enabled=all&name=grocery_cash)
- [Демолавки](https://tariff-editor.taxi.yandex-team.ru/experiments3/configs/show/demo_lavka/current?enabled=all&active=all&name=demo)

---

## Stands

| Environment | Lavka                                                                                                      | Deli                                             | Market                                                           |
|-------------|------------------------------------------------------------------------------------------------------------|--------------------------------------------------|------------------------------------------------------------------|
| stable      | [lavka.yandex.ru](https://lavka.yandex.ru)                                                                 | [deli.yango.com](https://deli.yango.com)         | [10min.market.yandex.ru](https://10min.market.yandex.ru)         |
| prestable   | [grocery-frontend-standalone-pre.lavka.yandex.ru](https://grocery-frontend-standalone-pre.lavka.yandex.ru) | [deli-pre.yango.com](https://deli-pre.yango.com) | [10min-pre.market.yandex.ru](https://10min-pre.market.yandex.ru) |

| Environment | Lavka                                                                                                      | Deli                                                                   | Market                                                                                 |
|-------------|------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| testing     | [grocery-frontend-standalone.lavka.tst.yandex.ru](https://grocery-frontend-standalone.lavka.tst.yandex.ru) | [deli.tst.yango.com](https://deli.tst.yango.com)                       | [market.lavka.tst.yandex.ru](https://market.lavka.tst.yandex.ru)                       |
| unstable    | [unstable.lavka.dev.yandex.ru](https://unstable.lavka.dev.yandex.ru)                                       | [unstable.deli.dev.yango.com](https://unstable.deli.dev.yango.com)     | [unstable.market.lavka.dev.yandex.ru](https://unstable.market.lavka.dev.yandex.ru)     |

| Environment | Lavka                                                                                                      | Deli                                                                   | Market                                                                                 |
|-------------|------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| amnesia     | [amnesia.lavka.dev.yandex.ru](https://amnesia.lavka.dev.yandex.ru)                                         | [amnesia.deli.dev.yango.com](https://amnesia.deli.dev.yango.com)       | [amnesia.market.lavka.dev.yandex.ru](https://amnesia.market.lavka.dev.yandex.ru)       |
| blueberry   | [blueberry.lavka.dev.yandex.ru](https://blueberry.lavka.dev.yandex.ru)                                     | [blueberry.deli.dev.yango.com](https://blueberry.deli.dev.yango.com)   | [blueberry.market.lavka.dev.yandex.ru](https://blueberry.market.lavka.dev.yandex.ru)   |
| bubblegum   | [bubblegum.lavka.dev.yandex.ru](https://bubblegum.lavka.dev.yandex.ru)                                     | [bubblegum.deli.dev.yango.com](https://bubblegum.deli.dev.yango.com)   | [bubblegum.market.lavka.dev.yandex.ru](https://bubblegum.market.lavka.dev.yandex.ru)   |
| candyland   | [candyland.lavka.dev.yandex.ru](https://candyland.lavka.dev.yandex.ru)                                     | [candyland.deli.dev.yango.com](https://candyland.deli.dev.yango.com)   | [candyland.market.lavka.dev.yandex.ru](https://candyland.market.lavka.dev.yandex.ru)   |
| haze        | [haze.lavka.dev.yandex.ru](https://haze.lavka.dev.yandex.ru)                                               | [haze.deli.dev.yango.com](https://haze.deli.dev.yango.com)             | [haze.market.lavka.dev.yandex.ru](https://haze.market.lavka.dev.yandex.ru)             |
| indica      | [indica.lavka.dev.yandex.ru](https://indica.lavka.dev.yandex.ru)                                           | [indica.deli.dev.yango.com](https://indica.deli.dev.yango.com)         | [indica.market.lavka.dev.yandex.ru](https://indica.market.lavka.dev.yandex.ru)         |
| larilena    | [larilena.lavka.dev.yandex.ru](https://larilena.lavka.dev.yandex.ru)                                       | [larilena.deli.dev.yango.com](https://larilena.deli.dev.yango.com)     | [larilena.market.lavka.dev.yandex.ru](https://larilena.market.lavka.dev.yandex.ru)     |
| mjay        | [mjay.lavka.dev.yandex.ru](https://mjay.lavka.dev.yandex.ru)                                               | [mjay.deli.dev.yango.com](https://mjay.deli.dev.yango.com)             | [mjay.market.lavka.dev.yandex.ru](https://mjay.market.lavka.dev.yandex.ru)             |
| notasha     | [notasha.lavka.dev.yandex.ru](https://notasha.lavka.dev.yandex.ru)                                         | [notasha.deli.dev.yango.com](https://notasha.deli.dev.yango.com)       | [notasha.market.lavka.dev.yandex.ru](https://notasha.market.lavka.dev.yandex.ru)       |
| sativa      | [sativa.lavka.dev.yandex.ru](https://sativa.lavka.dev.yandex.ru)                                           | [sativa.deli.dev.yango.com](https://sativa.deli.dev.yango.com)         | [sativa.market.lavka.dev.yandex.ru](https://sativa.market.lavka.dev.yandex.ru)         |
| strawberry  | [strawberry.lavka.dev.yandex.ru](https://strawberry.lavka.dev.yandex.ru)                                   | [strawberry.deli.dev.yango.com](https://strawberry.deli.dev.yango.com) | [strawberry.market.lavka.dev.yandex.ru](https://strawberry.market.lavka.dev.yandex.ru) |

| Environment | Lavka                                                  | Deli                                                 | Market                                                               |
|-------------|--------------------------------------------------------|------------------------------------------------------|----------------------------------------------------------------------|
| dev         | [lavka.local.yandex.ru](https://lavka.local.yandex.ru) | [deli.local.yango.com](https://deli.local.yango.com) | [https://10min.local.market.yandex.ru](10min.local.market.yandex.ru) |

---

## Client metrics

| Service      | Stable                                              | Testing                                                  |
|--------------|-----------------------------------------------------|----------------------------------------------------------|
| ErrorBooster | https://error.yandex-team.ru/projects/lavkaweb      | https://error.yandex-team.ru/projects/lavkaweb_test      |
| RUM          | https://rum.yandex-team.ru/projects/lavkaweb        | https://rum.yandex-team.ru/projects/lavkaweb_test        |
| Events       | https://events.chv.yandex-team.ru/projects/lavkaweb | https://events.chv.yandex-team.ru/projects/lavkaweb_test |
| Metrika      | https://metrika.yandex.ru/dashboard?id=62173660     | https://metrika.yandex.ru/dashboard?id=86909879          |

---

## TeamCity

### Выкатить релиз

- [Дока](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/release/)
- [Сборка в TeamCity](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_FrontendMonorepo_Stable&branch_YandexTaxiProjects_Infranaim_Frontend=lavka-grocery-frontend-standalone&tab=buildTypeStatusDiv)

### Выкатить хотфикс

- [Дока](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/release/xotfiks/)
- [Сборка в TeamCity](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_Infranaim_Frontend_Hotifx&branch_YandexTaxiProjects_Infranaim_Frontend=lavka-grocery-frontend-standalone&tab=buildTypeStatusDiv)

---

## Логи

### Kibana

[Маппинг ключей Кибаны](https://nda.ya.ru/t/iCWq65eU4JNiWY)

| Environment | Link                               |
|-------------|------------------------------------|
| testing     | https://nda.ya.ru/t/ILtUP7rB4aCs7Y |
| production  | https://nda.ya.ru/t/16OtgWAk4aCtCv |

---

## Графики и алерты

### Grafana

#### Графики

| Environment | Настроенные графики                                                                                | Автоматика                                                                                         |
|-------------|----------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| testing     | [Link](https://grafana.yandex-team.ru/d/hHwLEb4Gz/nanny_lavka_grocery-frontend-standalone_testing) | [Link](https://grafana.yandex-team.ru/d/hHwLEb4Gz/nanny_lavka_grocery-frontend-standalone_testing) |
| production  | [Link](https://grafana.yandex-team.ru/d/RkSA49pnk/lavkaweb-dashboard)                              | [Link](https://grafana.yandex-team.ru/d/hHwLEb4Gz/nanny_lavka_grocery-frontend-standalone_stable)  |

#### Конфиги

| Environment | Grafana config                                                                                                                       | Droblu config                                                                                                                             |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| testing     | [Link](https://github.yandex-team.ru/taxi/infra-cfg-graphs/blob/master/grafana/nanny_lavka_grocery-frontend-standalone_testing.yaml) | [Link](https://github.yandex-team.ru/taxi/infra-cfg-graphs/blob/master/dorblu/lavka/nanny.lavka_grocery-frontend-standalone_testing.yaml) |
| production  | [Link](https://github.yandex-team.ru/taxi/infra-cfg-graphs/blob/master/grafana/nanny_lavka_grocery-frontend-standalone_stable.yaml)  | [Link](https://github.yandex-team.ru/taxi/infra-cfg-graphs/blob/master/dorblu/lavka/nanny.lavka_grocery-frontend-standalone_stable.yaml)  |

### Juggler

| Environment | Monitoring                                                                                                                             | Config                                                                                                                                        |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| testing     | [Link](https://juggler.yandex-team.ru/aggregate_checks/?project=taxi.lavka.test&query=host%3Dlavka_grocery-frontend-standalone_stable) | [Link](https://github.yandex-team.ru/taxi/infra-cfg-juggler/blob/master/checks/taxi.lavka.test/rtc_lavka_grocery-frontend-standalone_testing) |
| production  | [Link](https://juggler.yandex-team.ru/aggregate_checks/?project=taxi.lavka.prod&query=host%3Dlavka_grocery-frontend-standalone_stable) | [Link](https://github.yandex-team.ru/taxi/infra-cfg-juggler/blob/master/checks/taxi.lavka.prod/rtc_lavka_grocery-frontend-standalone_stable)  |

- [Telegram alert config](https://github.yandex-team.ru/taxi/infra-cfg-juggler/blob/master/telegram_options)
- [Error Booster alerts](https://juggler.yandex-team.ru/notification_rules/?query=project%3Derror-booster-alerts%26tag%3Derror-booster-project-lavkaweb)
- [Проект в Monitoring](https://monitoring.yandex-team.ru/projects/lavkagroceryfrontendstandalone)

### Особые графики

- [Заказы](https://grafana.yandex-team.ru/d/-1vwpu-Gz/grocery-orders-dashboard-production?orgId=1&refresh=30s&var-country=All&var-app_name=Grocery%20Desktop&from=now-2d&to=now)
- [Посылки в маркете](<https://grafana.yandex-team.ru/d/UfpWYmd7k/tristero-backend?orgId=1&from=now-2d&to=now&var-names=All&var-country=All&var-app_name=TurboApp%20(android)&var-app_name=Grocery%20Desktop&refresh=1m>)
