# Зоны ответственности

Небольшая сводная табличка про то, кто за какие сервисы отвечает внутри службы.
Чтобы было проще понять к кому идти с проблемами сервисов.
Не показывайте, пожалуйста эту табличку наружу.

Сервис | Первый ответственный | Второй ответственный | Документация
:---: | :---: | :---: | :---:
Аудиты (SOX/PCIDSS) |  [@fresk](https://staff.yandex-team.ru/fresk) | [@r-vishnevsky](https://staff.yandex-team.ru/r-vishnevsky) | [wiki](https://wiki.yandex-team.ru/verticals/sox-changes/)
Доп договоры с Cloud | [@ibiryulin](https://staff.yandex-team.ru/ibiryulin) | [@r-vishnevsky](https://staff.yandex-team.ru/r-vishnevsky)
Capacity planning/распределение квот | [@ibiryulin](https://staff.yandex-team.ru/ibiryulin) | [@r-vishnevsky](https://staff.yandex-team.ru/r-vishnevsky)
CME infra on dualstack | [@mariausova](https://staff.yandex-team.ru/mariausova) | [@a-a-ovcharov](https://staff.yandex-team.ru/a-a-ovcharov) [@a-v-zelenin](https://staff.yandex-team.ru/a-v-zelenin)
CME infra | [@a-a-ovcharov](https://staff.yandex-team.ru/a-a-ovcharov) | [@a-v-zelenin](https://staff.yandex-team.ru/a-v-zelenin)
Переливки баз | [@opyakin-roman](https://staff.yandex-team.ru/opyakin-roman) | [@r-vishnevsky](https://staff.yandex-team.ru/r-vishnevsky) | [wiki](https://wiki.yandex-team.ru/vertis-admin/storage/Perelivka-v-YT/)
mysql | [@r-vishnevsky](https://staff.yandex-team.ru/r-vishnevsky) | [@opyakin-roman](https://staff.yandex-team.ru/opyakin-roman) | [wiki](https://wiki.yandex-team.ru/vertis-admin/storage/mysql/)
couchbase | [@wf1nder](https://staff.yandex-team.ru/wf1nder) | [@r-vishnevsky](https://staff.yandex-team.ru/r-vishnevsky) | [wiki](https://wiki.yandex-team.ru/vertis-admin/storage/couchbase/)
cassandra | [@r-vishnevsky](https://staff.yandex-team.ru/r-vishnevsky)| [@wf1nder](https://staff.yandex-team.ru/wf1nder) | [wiki](https://wiki.yandex-team.ru/vertis-admin/storage/cassandra/)
zookeeper | [@opyakin-roman](https://staff.yandex-team.ru/opyakin-roman) | [@wf1nder](https://staff.yandex-team.ru/wf1nder) | [новый](https://wiki.yandex-team.ru/vertis-admin/Zookeeper/) [старый](https://wiki.yandex-team.ru/vertis-admin/zookeeper-old/)
wall-e | [@kasev](https://staff.yandex-team.ru/kasev) | [@ibiryulin](https://staff.yandex-team.ru/ibiryulin) | [docs](iaas/metal-server-management.md#zheleznye-docker-servera)
docker/nomad/consul/registry | [@kasev](https://staff.yandex-team.ru/kasev) | [@mariausova](https://staff.yandex-team.ru/mariausova) | [docs](https://docs.yandex-team.ru/classifieds-ops-internal/services/internal-cloud/nomad-system-and-jobs)
envoy+envoy-api | [@kasev](https://staff.yandex-team.ru/kasev) | [@danevge](https://staff.yandex-team.ru/danevge)
yandex-cloud+terraform | [@kasev](https://staff.yandex-team.ru/kasev) | [@mariausova](https://staff.yandex-team.ru/mariausova) | [docs](https://docs.yandex-team.ru/classifieds-ops-internal/iaas/terraform)
rundeck | [@r-vishnevsky](https://staff.yandex-team.ru/r-vishnevsky) | [@wf1nder](https://staff.yandex-team.ru/wf1nder) | [wiki](https://wiki.yandex-team.ru/vertis-admin/rundeck/)
jenkins | [@wf1nder](https://staff.yandex-team.ru/wf1nder) | [@kasev](https://staff.yandex-team.ru/kasev) | [docs](services/ci/jenkins.md)
sentry | [@wf1nder](https://staff.yandex-team.ru/wf1nder) | [@r-vishnevsky](https://staff.yandex-team.ru/r-vishnevsky) | [docs](services/metrics-and-monitoring/sentry.md)
teamcity | [@mariausova](https://staff.yandex-team.ru/mariausova) | [@wf1nder](https://staff.yandex-team.ru/wf1nder) | [сервер](services/ci/teamcity.md) [агенты](services/ci/teamcity-agents.md)
gh actions | [@mariausova](https://staff.yandex-team.ru/mariausova) | [@wf1nder](https://staff.yandex-team.ru/wf1nder) | [docs](services/ci/github-runners.md)
victoria metrics/grafana/graphite | [@wf1nder](https://staff.yandex-team.ru/wf1nder) | [@opyakin-roman](https://staff.yandex-team.ru/opyakin-roman) | [docs](services/metrics-and-monitoring/vm.md)
kafka | [@wf1nder](https://staff.yandex-team.ru/wf1nder) | [@r-vishnevsky](https://staff.yandex-team.ru/r-vishnevsky) | [MDB](services/storages/kafka/mdb.md) [железная](https://wiki.yandex-team.ru/vertis-admin/kafka/)
nginx | [@opyakin-roman](https://staff.yandex-team.ru/opyakin-roman) | [@ibiryulin](https://staff.yandex-team.ru/ibiryulin) | [docs](https://docs.yandex-team.ru/classifieds-ops-internal/services/network/nginx/configuration)
squid | [@ibiryulin](https://staff.yandex-team.ru/ibiryulin) | [@kasev](https://staff.yandex-team.ru/kasev) | [docs](https://docs.yandex-team.ru/classifieds-infra/external-proxy)
tableau | [@wf1nder](https://staff.yandex-team.ru/wf1nder) | [@r-vishnevsky](https://staff.yandex-team.ru/r-vishnevsky) | [docs](services/metrics-and-monitoring/tableau.md)
memcached  | [@wf1nder](https://staff.yandex-team.ru/wf1nder) | [@ibiryulin](https://staff.yandex-team.ru/ibiryulin)
gearman | [@ibiryulin](https://staff.yandex-team.ru/ibiryulin)
sphinx | [@ibiryulin](https://staff.yandex-team.ru/ibiryulin)
vipnet | [@kasev](https://staff.yandex-team.ru/kasev) | | [wiki](https://wiki.yandex-team.ru/vertis-admin/pro-vipnet-v-vertikaljax/)
СМЭВ | [@kasev](https://staff.yandex-team.ru/kasev) | | [docs](other/rostelecom/rostelecom-proxy.md)
aptly | [@opyakin-roman](https://staff.yandex-team.ru/opyakin-roman) | [@kasev](https://staff.yandex-team.ru/kasev) | [docs](iaas/aptly.md)
h2p | [@opyakin-roman](https://staff.yandex-team.ru/opyakin-roman) | [@danevge](https://staff.yandex-team.ru/danevge) | [пользовательская](https://docs.yandex-team.ru/classifieds-infra/h2p/quick-start) [архитектура](https://wiki.yandex-team.ru/vertis-admin/Архитектура-h2p/)
hub | [@danevge](https://staff.yandex-team.ru/danevge) | [@ibiryulin](https://staff.yandex-team.ru/ibiryulin) |
db-consul-discovery | [@opyakin-roman](https://staff.yandex-team.ru/opyakin-roman) | [@danevge](https://staff.yandex-team.ru/danevge) | [wiki](https://wiki.yandex-team.ru/vertis-admin/storage/db-consul-discovery/)
sender-proxy | [@danevge](https://staff.yandex-team.ru/danevge) | [@niklogvinenko](https://staff.yandex-team.ru/niklogvinenko)
[jaeger](https://wiki.yandex-team.ru/vertis-admin/tracing/) | [@makw19](https://staff.yandex-team.ru/makw19) | [@danevge](https://staff.yandex-team.ru/danevge)
[logs](https://wiki.yandex-team.ru/vertis-admin/logs/) | [@makw19](https://staff.yandex-team.ru/makw19) | [@danevge](https://staff.yandex-team.ru/danevge)
[shiva](https://docs.yandex-team.ru/classifieds-infra/deploy) | [@niklogvinenko](https://staff.yandex-team.ru/niklogvinenko) | [@danevge](https://staff.yandex-team.ru/danevge)
cms | [@opyakin-roman](https://staff.yandex-team.ru/opyakin-roman) | [@ibiryulin](https://staff.yandex-team.ru/ibiryulin) | [docs](https://docs.yandex-team.ru/classifieds-ops-internal/services/internal-cloud/cms)

Дата актуализации: Jun 7 14:06:07
