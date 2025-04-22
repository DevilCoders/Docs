# Автоматическая сборка и деплоймент в Arcadia CI (CI/CD)

## Общее
В Крипте в процессе разработки используются стандартные яндексовые системы:
1. [Аркадия](https://a.yandex-team.ru/arcadia/crypta) как репозиторий
2. [ya.make + ya make](https://docs.yandex-team.ru/ya-make/) для сборки и тестирования бэкенда или внешний [npm](https://www.npmjs.com) для сборки веб-фронтенда
3. [package.json + ya package](https://docs.yandex-team.ru/devtools/package) для пакетирования, в т.ч. Docker образов
4. [Sandbox](https://docs.yandex-team.ru/sandbox/) как облачная среда для выполнения задач сборки
5. [Arcadia CI](https://docs.yandex-team.ru/ci/) или [Цум](https://tsum.yandex-team.ru/pipe/projects/crypta) для построения пайплайнов сборки, релиза и деплоя
6. [Deploy](https://deploy.yandex-team.ru) (редко [Nanny](https://docs.yandex-team.ru/nanny/)) для деплоя сервисов, [Sandbox](https://docs.yandex-team.ru/sandbox/) (редко [Nirvana](https://docs.yandex-team.ru/nirvana/)) для запуска задач

## Работа с Arcadia CI
Ссылки:
* [Документация](https://docs.yandex-team.ru/ci/)
* [UI](https://a.yandex-team.ru/projects/all?text=crypta) - рекомендую добавить все Крипта-проекты в избранное
* Общая конфигурация Крипты в Аркадии: [crypta/ci](https://a.yandex-team.ru/arcadia/crypta/ci) 
* Общие таски сборки (обертки Sandbox задач) Крипты в CI Registry: [ci/registry/projects/crypta](https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/projects/crypta)  
* Общий секрет со всеми необходимыми для сборки токенами: [Vault](https://yav.yandex-team.ru/secret/sec-01efps66gnbmejg9wvc9ptvhmc/explore/versions)  

Вся конфигурация сборки делается в [a.yaml](https://docs.yandex-team.ru/ci/example) файлах.

CI/CD пайплайны делятся на:
- **Прекоммитные** чеки (**action**), которые выполняются на этапе создания Pull Request. Это могут быть проверки правильности конфигурации, у нас туда вынесены очень большие тесты, не влезающие в автосборку. Из-за ограничений Arcadia CI такие a.yaml файлы находятся в директории с проектом.
- **Посткоммитные** действия (action) и релизные сборки (release), выполняются после коммита в trunk. Рекомендуется размещать такие файлы в директории [crypta/ci](https://a.yandex-team.ru/arcadia/crypta/ci). Хранение в едином месте позволяет сделать более читаемый UI и лучше переиспользовать код.
  - **Action** - нужны для кастомных действий и для применения configuration as code (см. [Spine](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/lib/python/spine/README.md)) и др.
  - **Release** - нужны для сборки, релиза и деплоймента пакетов и сопутствующих действий, как то создание релизных тикетов и уведомлений, запуск постерелизных чеков

Чтобы создать релизный пайплайн своего проекта, нужно:
1. Создать соответствующий package.json в своём проекте
2. Создать новый или обновить существующий a.yaml в [crypta/ci](https://a.yandex-team.ru/arcadia/crypta/ci) по аналогии
3. Если a.yaml новый, привязать к наиболее подходящему по смыслу [ABC-сервису Крипты](https://abc.yandex-team.ru/services/cryptaall/services/)
4. Корректно настроить фильтры срабатывания сборки. Сейчас мы используем фильтры по абсолютным путям из-за временного [отсутствия](https://st.yandex-team.ru/CI-2844) фильтров на graph discovery.
5. Если нужно запускать нестандартные задачи сборки, то можно создать новый тип таски или переиспользовать существующий из [общего](https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/common) или [криптового](https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/projects/crypta) CI Registry. Часто для задачи нужен токен для robot-crypta в той системе, с которой он взаимодействует. Нужно проверить наличие или добавить в [общем секрете](https://yav.yandex-team.ru/secret/sec-01efps66gnbmejg9wvc9ptvhmc/explore/versions)
6. Создать PR и изменениями, прекоммитный чек быстро проверит корректность измененных a.yaml 
7. После коммита конфигурация почти моментально появится в [UI](https://a.yandex-team.ru/projects/all?text=crypta) в соотвествующем ABC-сервисе
8. Обязательно запустить сборку и проверить её работоспособность. Это можно сделать, добавив коммит вручную.

### Переиспользуемые компоненты
#### Tasks
В CI Registry есть набор тасок (оберток вокруг Sandbox) Крипты с заданными дефолтными параметрами сборки, требований к энву и уведомлений.
- [ya_package](https://a.yandex-team.ru/arcadia/ci/registry/projects/crypta) - ya_package с дефолтными параметрами для сборки tar.gz архива, который кладётся в Sandbox под определенными именем ресурса
- [ya_package_docker](https://a.yandex-team.ru/arcadia/ci/registry/projects/crypta) - ya_package с дефолтными параметрами для сборки docker
- [ya_make_yt](https://a.yandex-team.ru/arcadia/ci/registry/projects/crypta/graph/crypta_ya_make_yt.yaml) - позволяет собрать программу с помощь ya make, но сложить результат не как sandbox ресурс, а на YT. Используется для сборки YQL UDF


#### YAML anchor
Пока в CI [нет возможности](https://st.yandex-team.ru/CI-2426) переиспользовать код между разными a.yaml файлами, но внутри одного a.yaml мождно использовать [YAML Anchor](https://support.atlassian.com/bitbucket-cloud/docs/yaml-anchors/) - возможность вставлять кусок yaml в другое место.
Используем в основном для переиспользования stages, т.к. многие релизы включают в себя автоматическую сборку + ручной релиз.

#### Flows
Flow - цепочка выполнения джобов, часто повторяется. Есть возможность написать flow 1 раз и переиспользовать его, переопределяя `flow-vars` (пока только в пределах одного a.yaml, поэтому даже стандартные flow копипастятся между конфигурациями). Наши стандартные flow:
- [crypta-build-and-release](https://a.yandex-team.ru/search?search=crypta-build-and-release,%5Ecrypta%2Fci%2F.*,,arcadia,,200&repo=arcadia) - собрать ресурс с помощью `ya_package` и зарелизить в определенный статус
- [deploy-docker-flow](https://a.yandex-team.ru/search?search=deploy-docker-flow,%5Ecrypta%2Fci%2F.*,,arcadia,,200&repo=arcadia) - собрать докер контейнер, залить в докер-репозиторий и задеплоить в Deploy с помощью [deploy:create_release](https://a.yandex-team.ru/arcadia/ci/registry/common/deploy)

#### package_build_deps
- [package_build_deps](https://a.yandex-team.ru/search?search=package_build_deps,%5Ecrypta%2F.*,,arcadia,,200&repo=arcadia) - утилита, позволяющая создать правильные фильтры срабатывания сборки и сделать тесты на расхождение фильтров реальным зависимостям. Сейчас не работает, требуется [переделка](https://st.yandex-team.ru/CRYPTA-15125) 
