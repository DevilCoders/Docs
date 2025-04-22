# Пользовательские сигналы

Сейчас доступны следующие виды сигналов:

1) Системные сигналы с pod_agent для команды разработчиков
1) [Сигналы с пользовательских контейнеров](containers.md), сейчас они считаются системными, но в будущем будут перенесены в пользовательскую квоту.
1) [Сигналы о состоянии объектов внутри пода](objectconditions.md) Сигналы не будут работать до анонса второго endpoint https://st.yandex-team.ru/DEPLOY-2045
1) [Сигналы с пользовательских http/tcp проверок/действий](network-actions.md) Сигналы не будут работать до анонса второго endpoint https://st.yandex-team.ru/DEPLOY-2045

##  Как найти сигналы {#location}

В рамках [https://st.yandex-team.ru/DEPLOY-2045](https://st.yandex-team.ru/DEPLOY-2045) в этом пункте произойдут изменения.

У сигналов проставлены следующие `itype` и `prj`:

```bash
itype=pod_agent;
prj=<stage_id>.<deploy_unit_id>
signals=unistat-<signal_name>;
hosts=ASEARCH;
```

В качестве `hosts` можно указывать `ASEARCH`, тогда поиск сигналов будет произведен по всем хостам, а также можно указать конкретный хост.

Все сигналы имеют префикс `unistat-`.

[Например сигналов с одного из тестовых подов деплоя.](https://yasm.yandex-team.ru/chart/signals=unistat-container_workload_TestBoxInitCmdWorkload_readiness_exited_deee;hosts=ASEARCH;itype=pod_agent;prj=pod-agent-test-stage-on-xdc.main-deploy-unit/)

##  Лимит на сигналы {#limit}
Из-за лимита на количество сигналов с одного пода, который равен 2000, при очень большом количестве объектов в спеке часть пользовательских сигналов может не доходить до yasm.

В данный момент:

1) Около 60 сигналов заняты системой
1) На каждый контейнер внутри пода (`box init`, `workload start/init/readiness/liveness/stop/destroy`) генерируется по 7 дополнительных сигналов
1) На каждый объект в спеке пода генерируется по 3 дополнительных сигнала <[Сигналы не будут добавляться до анонса второго endpoint https://st.yandex-team.ru/DEPLOY-2045]>
1) На каждую http проверку/действие (`workload readiness/liveness/stop/destroy`) генерируется 4 дополнительных сигнала <[Сигналы не будут добавляться до анонса второго endpoint https://st.yandex-team.ru/DEPLOY-2045]>
1) На каждую tcp проверку (`workload readiness/liveness`) генерируется 3 дополнительных сигнала <[Сигналы не будут добавляться до анонса второго endpoint https://st.yandex-team.ru/DEPLOY-2045]>

Сигналы добавляются только тогда, когда объект реально есть в спеке, например, если у вас есть `workload` с 2 `init` командами, `http readiness`, `tcp liveness`, `container stop`, без указания `destroy policy`, то за него будет добавлено:

`7 (for start container) + 14 (for 2 init containers) + 4 (for readiness http check) + 3 (for liveness tcp check) + 7 (for container stop) + 0 (for no destroy)`
