# Deployment

## Ссылки

Запущено в Y.Deploy:

- [nocrfcsd-production-stage](https://deploy.yandex-team.ru/stages/nocrfcsd-production-stage)
- [nocrfcsd-testing-stage](https://deploy.yandex-team.ru/stages/nocrfcsd-testing-stage)

Секретница: [sec-01fkdmk2r9dbsy1f53efb4d8bs](https://yav.yandex-team.ru/secret/sec-01fkdmk2r9dbsy1f53efb4d8bs/)

Макрос: [_NOCRFCSDNETS_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_NOCRFCSDNETS_)

Балансеры L3 и L7:

- [nocrfcs-api.yandex-team.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/nocrfcs-api.yandex.net/)
- [nocrfcs-api-test.yandex-team.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/nocrfcs-api-test.yandex-team.ru/)

DNS:

- production: [DNSREQUESTS-2846](https://st.yandex-team.ru/DNSREQUESTS-2846)
- testing: [DNSREQUESTS-2870](https://st.yandex-team.ru/DNSREQUESTS-2870)

Кластер PostgreSQL:
[nocrfcsd](https://yc.yandex-team.ru/folders/foosk13mu0ib9qrjkh8a/managed-postgresql/cluster/mdb32tclap69oi41k607)

Релизы: [Release nocrfcsd](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Fnocrfcsd&id=nocrfcsd)

Исходники: [nocrfcsd](https://a.yandex-team.ru/arc_vcs/noc/nocrfcsd)

Предыдущие исходники: - [https://noc-gitlab.yandex-team.ru/korxif/nocrfc](https://noc-gitlab.yandex-team.ru/korxif/nocrfc)

Дырки в Puncher:

- [доступ сотрудников к API](https://st.yandex-team.ru/DOSTUPREQ-270217)
- [приём вебхуков от Startrek](https://st.yandex-team.ru/DOSTUPREQ-270874)
- [доступ в infra](https://st.yandex-team.ru/DOSTUPREQ-269115)
- [доступ в calendar](https://st.yandex-team.ru/DOSTUPREQ-269116)

Форма:

- production: [Запрос на изменение (NOCRFCS)](https://forms.yandex-team.ru/surveys/21525/)
- testing: пока нет

Очереди в Startrek:

- production: [NOCRFCS](https://st.yandex-team.ru/NOCRFCS)
- testing: [NOCRFCSTEST](https://st.yandex-team.ru/NOCRFCSTEST)

TVM:

- production:
  - ресурс: [nocrfcsd](https://abc.yandex-team.ru/services/netauto/resources/?view=consuming&layout=table&supplier=14&show-resource=40442322)
  - TVM Service ID: `2032816`
- testing:
  - ресурс: [nocrfcsd тестинг](https://abc.yandex-team.ru/services/netauto/resources/?view=consuming&layout=table&supplier=14&show-resource=40446305)
  - TVM Service ID: `2032822`
