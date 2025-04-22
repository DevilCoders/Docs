# market-teamcity

## Описание
Представляет из себя набор модулей и образов, которые необходимы для сборок проектов Маркета:

### Докер образы
#### Билд агент
* [Скрипты для шаблона единой сборки](https://teamcity.yandex-team.ru/admin/editBuild.html?id=template:MarketInfra_Sandbox_MarketJavaDeployProject) ( [Wiki](https://wiki.yandex-team.ru/users/vladvin/Nastrojjka-sborki-v-Teamcity-na-baze-obshhego-shablona/) )
* Скрипты мультитестингов

#### Образ для запуска докера из докера

#### Пример репозитория с использование докера из докера

### Деб пакеты
#### yandex-market-infra-teamcity-agent
Пакет для обновления докер-образов на железных машинках <br>
После первой установки нужно порестартить Docker.

### Прочие скрипты
* Скрипты частей сборок MBO и MBI

## Релиз
[Релизится пайплайном](https://tsum.yandex-team.ru/pipe/projects/infra/release/new/teamcity-agents)
