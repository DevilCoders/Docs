# Lavka web

Веб-версия Яндекс.Лавки<br/>
Документация по разработке на [Вики](https://wiki.yandex-team.ru/lavka/web/)

---

## Documentation

- [CONTRIBUTING](docs/CONTRIBUTING.md)
- [Styleguide](docs/styleguide.md)
- [Как писать a11y код](docs/a11y.md)
- [Переводы](.tanker/README.md)
- [Нагрузочное тестирование](.load-testing/README.md)
- [Релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/release/)

---

## Ссылки

### Общие
- [Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/35/edit/354720/info)
- [Figma](https://www.figma.com/file/PJG55GXBl8cYdcN2AnFMnF/Десктоп?node-id=1568%3A202)
- [GAP Config](https://tariff-editor.taxi.yandex-team.ru/authproxies/grocery-authproxy/show/LzQuMC9ncm9jZXJ5LXN1cGVyYXBwL2xhdmth)

### По окружению
| Service      | Stable                              | Testing                                           |
| ------------ | ----------------------------------- | ------------------------------------------------- |
| CSP | https://csp.yandex-team.ru/projects/lavkaweb | https://csp.yandex-team.ru/projects/lavkaweb_test |

---

## Experiments and Configs

| Environment | Experiments                                                                                                                                       | Configs                                                                                                                                       |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| testing     | [Link](https://tariff-editor.taxi.tst.yandex-team.ru/experiments3/experiments?enabled=all&active=all&order=name_desc&name=lavka-frontend_desktop) | [Link](https://tariff-editor.taxi.tst.yandex-team.ru/experiments3/configs?enabled=all&active=all&order=name_desc&name=lavka-frontend_desktop) |
| stable      | [Link](https://tariff-editor.taxi.yandex-team.ru/experiments3/experiments?active=all&enabled=all&name=lavka-frontend_desktop)                     | [Link](https://tariff-editor.taxi.yandex-team.ru/experiments3/configs?active=all&enabled=all&name=lavka-frontend_desktop)                     |

### Особые эксперименты и конфиги

- [Специальные лавки](https://tariff-editor.taxi.yandex-team.ru/experiments3/configs/show/overlord_depots_hidings/current?active=all&enabled=all&name=overlord_depots_hidings)
- [Зоны](https://tariff-editor.taxi.yandex-team.ru/experiments3/experiments/show/grocery_geo_onboarding/current?enabled=all&active=all&name=grocery_geo_onboarding)
- [Кешбек](https://tariff-editor.taxi.yandex-team.ru/experiments3/experiments/show/grocery_cashback/current?active=all&enabled=all&name=grocery_cash)
- [Демолавки](https://tariff-editor.taxi.yandex-team.ru/experiments3/configs/show/demo_lavka/current?enabled=all&active=all&name=demo)

---

## Stands

| Environment | Lavka                                                   | Deli                                 | Market                                       |
| ----------- |---------------------------------------------------------| -------------------------------------|----------------------------------------------|
| dev         | https://lavka.local.yandex.ru                           | https://deli.local.yango.com         | https://10min.local.market.yandex.ru         |
| unstable    | https://unstable.lavka.dev.yandex.ru                    | https://unstable.deli.dev.yango.com  | https://unstable.market.lavka.dev.yandex.ru  |
| blueberry   | https://blueberry.lavka.dev.yandex.ru/                  | https://blueberry.deli.dev.yango.com | https://blueberry.market.lavka.dev.yandex.ru |
| indica      | https://indica.lavka.dev.yandex.ru/                     | https://indica.deli.dev.yango.com    | https://indica.market.lavka.dev.yandex.ru    |
| larilena    | https://larilena.lavka.dev.yandex.ru                    | https://larilena.deli.dev.yango.com  | https://larilena.market.lavka.dev.yandex.ru  |
| mjay        | https://mjay.lavka.dev.yandex.ru/                       | https://mjay.deli.dev.yango.com/     | https://mjay.market.lavka.dev.yandex.ru      |
| notasha     | https://notasha.lavka.dev.yandex.ru/                    | https://notasha.deli.dev.yango.com   | https://notasha.market.lavka.dev.yandex.ru   |
| sativa      | https://sativa.lavka.dev.yandex.ru/                     | https://sativa.deli.dev.yango.com    | https://sativa.market.lavka.dev.yandex.ru    |
| testing     | https://grocery-frontend-standalone.lavka.tst.yandex.ru | https://deli.tst.yango.com           | https://market.lavka.tst.yandex.ru           |
| prestable   | https://grocery-frontend-standalone-pre.lavka.yandex.ru | https://deli-pre.yango.com           | https://10min-pre.market.yandex.ru           |
| stable      | https://lavka.yandex.ru/                                | https://deli.yango.com               | https://10min.market.yandex.ru               |

---

## Client metrics

| Service      | Stable                                              | Testing                                                  |
| ------------ | --------------------------------------------------- | -------------------------------------------------------- |
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
| ----------- | ---------------------------------- |
| testing     | https://nda.ya.ru/t/ILtUP7rB4aCs7Y |
| stable      | https://nda.ya.ru/t/16OtgWAk4aCtCv |

---

## Графики и алерты

### Grafana

#### Графики

| Environment | Настроенные графики                                                                                | Автоматика                                                                                         |
| ----------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| testing     | [Link](https://grafana.yandex-team.ru/d/hHwLEb4Gz/nanny_lavka_grocery-frontend-standalone_testing) | [Link](https://grafana.yandex-team.ru/d/hHwLEb4Gz/nanny_lavka_grocery-frontend-standalone_testing) |
| stable      | [Link](https://grafana.yandex-team.ru/d/RkSA49pnk/lavkaweb-dashboard)                              | [Link](https://grafana.yandex-team.ru/d/hHwLEb4Gz/nanny_lavka_grocery-frontend-standalone_stable)  |

#### Конфиги

| Environment | Grafana config                                                                                                                       | Droblu config                                                                                                                             |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| testing     | [Link](https://github.yandex-team.ru/taxi/infra-cfg-graphs/blob/master/grafana/nanny_lavka_grocery-frontend-standalone_testing.yaml) | [Link](https://github.yandex-team.ru/taxi/infra-cfg-graphs/blob/master/dorblu/lavka/nanny.lavka_grocery-frontend-standalone_testing.yaml) |
| stable      | [Link](https://github.yandex-team.ru/taxi/infra-cfg-graphs/blob/master/grafana/nanny_lavka_grocery-frontend-standalone_stable.yaml)  | [Link](https://github.yandex-team.ru/taxi/infra-cfg-graphs/blob/master/dorblu/lavka/nanny.lavka_grocery-frontend-standalone_stable.yaml)  |

### Juggler

| Environment | Monitoring                                                                                                                             | Config                                                                                                                                        |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| testing     | [Link](https://juggler.yandex-team.ru/aggregate_checks/?project=taxi.lavka.test&query=host%3Dlavka_grocery-frontend-standalone_stable) | [Link](https://github.yandex-team.ru/taxi/infra-cfg-juggler/blob/master/checks/taxi.lavka.test/rtc_lavka_grocery-frontend-standalone_testing) |
| stable      | [Link](https://juggler.yandex-team.ru/aggregate_checks/?project=taxi.lavka.prod&query=host%3Dlavka_grocery-frontend-standalone_stable) | [Link](https://github.yandex-team.ru/taxi/infra-cfg-juggler/blob/master/checks/taxi.lavka.prod/rtc_lavka_grocery-frontend-standalone_stable)  |

- [Telegram alert config](https://github.yandex-team.ru/taxi/infra-cfg-juggler/blob/master/telegram_options)
- [Error Booster alerts](https://juggler.yandex-team.ru/notification_rules/?query=project%3Derror-booster-alerts%26tag%3Derror-booster-project-lavkaweb)
- [Проект в Monitoring](https://monitoring.yandex-team.ru/projects/lavkagroceryfrontendstandalone)

### Особые графики

- [Заказы](https://grafana.yandex-team.ru/d/-1vwpu-Gz/grocery-orders-dashboard-production?orgId=1&refresh=30s&var-country=All&var-app_name=Grocery%20Desktop&from=now-2d&to=now)
- [Посылки в маркете](<https://grafana.yandex-team.ru/d/UfpWYmd7k/tristero-backend?orgId=1&from=now-2d&to=now&var-names=All&var-country=All&var-app_name=TurboApp%20(android)&var-app_name=Grocery%20Desktop&refresh=1m>)
