# Взгляд сверху

Balancer deployer представляет собой исполняемый файл [написанный на python](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/balancer_deployer/), а также несколько sandbox-задач, которые запускают данный файл с различными параметрами.
<br>Каждая sandbox задача работает под взятым семафором [`MAPS_BALANCER_DEPLOYER`](https://sandbox.yandex-team.ru/admin/semaphores/27181514/view), чтобы исключить возможные гонки из-за одновременного выполнения задач.
<br>Так-же задачи проверяют флаг its [`maps::common::balancer_deployer`](https://nanny.yandex-team.ru/ui/#/its/locations/maps/common/), чтобы исключить выкатки балансеров во время отключений дц.

Далее рассмотрим, какие sandbox задачи есть:

### 1. MAPS_BALANCER_DEPLOYER
После того, как [SEDEM](https://docs.yandex-team.ru/sedem/) сгенерировал конфиги, команда сервиса ее пошипала и влила в транк, необходимо их доставить до awacs.

Данный компонент представлен sandbox-задачей [MAPS_BALANCER_DEPLOYER](https://sandbox.yandex-team.ru/tasks?children=false&hidden=true&type=MAPS_BALANCER_DEPLOYER) ([исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/infra/MapsBalancerDeployer/__init__.py))
<br>[Покоммитный запуск](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/maps/infra/sedem/DeployBalancers.yaml)
![Блок-схема](img/deploy.png)

### 2. MAPS_BALANCER_UNPAUSER
Это очень простая стадия - sandbox задача делает некоторые проверки, касательно того, может ли балансер быть снят с паузы или нет. Если может быть снят с паузы-снимает, вследствии чего, конфиги балансера выкатятся в новый ДЦ.
<br>Что проверяем:
- Предыдущий этап (ДЦ) выкатился не менее часа назад
- Балансер был поставлен на паузу нашей автоматикой

Данный компонент представлен sandbox-задачей [MAPS_BALANCER_UNPAUSER](https://sandbox.yandex-team.ru/tasks?children=true&type=MAPS_BALANCER_UNPAUSER&limit=20) ([исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/infra/MapsBalancerUnpauser/__init__.py))
<br>[Запуск происходит по расписанию](https://sandbox.yandex-team.ru/scheduler/25368/view), каждые пол часа.

![Блок-схема](img/unpause.png)

### 3. MAPS_BALANCER_PULLER
Нам очень хотелось бы, чтобы изменения делались только через нашу систему, но это не так. Изменения могут сделать команды сервисов руками или же команда awacs сделает важные массовые изменения.
<br>Эти изменения могут быть очень важными, поэтому появилась потребность синхронизировать изменения не только в прямую, но и в обратную сторону.


Данный компонент представлен sandbox-задачей [MAPS_BALANCER_PULLER](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=MAPS_BALANCER_PULLER) ([исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/infra/MapsBalancerPuller/__init__.py))
<br>[Запуск происходит по расписанию](https://sandbox.yandex-team.ru/scheduler/24211/view), каждый час.


### 4. MAPS_BALANCER_MONITORING
Следит за тем, что MAPS_BALANCER_UNPAUSER в срок снял все балансеры с паузы, иначе начинает гореть мониторинг.

Данный компонент представлен sandbox-задачей [MAPS_BALANCER_MONITORING](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=MAPS_BALANCER_MONITORING) ([исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/infra/MapsBalancerPauseMonitoring/__init__.py))
<br>[Запуск происходит по расписанию](https://sandbox.yandex-team.ru/scheduler/25330/view), каждые 15 минут.
