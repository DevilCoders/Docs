### Examples
* http://ya-resolve.sec.yandex.net/api/v1/resolve?success_only=1&value=procenkoeg
* http://ya-resolve.sec.yandex.net/api/v1/resolve?success_only=1&value=robot-pika&type=person
* http://ya-resolve.sec.yandex.net/api/v1/resolve?value=SECURITY_MTN_NETS

### Supported Types
* tvm (for tvm client id)
* macro
* fqdn
* ip_address (ipv4 and ipv6)
* mac_address
* bot_instance_number
* department (staff)
* service (abc)
* servicerole (abc)
* person (сотрудник/робот/зомбик)
* wiki (wiki-group)
* service_id (abc)

## For Development

### Build and push docker image
1. `gofmt -w .` - format the code
2. `ya make -t`
3. `cd docker` - go to docker build packager folder
4. `make` - build, tag with current time, push to registry

### Run locally
1. `cd cmd/ya_resolve` - go to cmd folder
2. Prepare staff and abc OAuth tokens according to `main.go` file header
3. `go run main.go` - go run
4. Wait server to initialize and go to `http://localhost:3333/api/v1/resolve?success_only=1&value=procenkoeg`

### TODO
* QYP vm owners like `atom-proc.sas.yp-c.yandex.net`
* abc and staff pagination
* Add DevOps to ABC service resolver: https://abc.yandex-team.ru/services/Logbroker/
* Add service role proirity for "HW Management" like here: https://abc.yandex-team.ru/services/portalnajastatika

### Checklists

Types of sources in puncher:
- https://wiki.yandex-team.ru/noc/nocdev/puncher/spravka/#3.zapolneniepolejjzajavki

Examples:
* yandex_content_geodev_tech (department)
* svc_mail (abc service)
* procenkoeg (staff person)
* zomb-secret (staff person robot)
* osipov-vadim (staff person fired person)
* adfox (abc service)
* svc_yc_iam_dev (abc service role)
* yandex_search_tech_quality_robot_dep38673 (department)
* yandex_exp_9053_3947 (department)
* robot-issue (robot ownage recursion)
* 2002104 (tvm)
* 95.108.142.117 (ip -> racktables_ip2mac_resolver -> mac -> bot_resolver -> abc_resource_external_id -> abc_service -> abc_servce_members)
* security-burp-collaborator-prod-burp.stable.qloud-b.yandex.net (racktables owners endpoint)
* mtsyslog01e.yandex.ru (walle)
* nessus-3.sec.yandex.net (walle, 1 more check)
* SECURITY_MTN_NETS (racktables owners resolver macro)
* _SECURITY_MTN_NETS_ (racktables owners resolver macro)
* 87.250.253.82 (ip --racktables_ip2macro--> macro --racktables_owners_macro--> ...)
* 909 (abc service id)
* molly-collector.sec.yandex.net  (over puncher api)

Problematic examples (dont work):
* vlegeza (faired person. Removed staff department. No department head)
* clyo-dev (What is this? How to resolve it? Split by delimeters is ok?)
* `2a02:6b8:c04:248:0:522:a2f:5707`
* `buildagent-mac-sas-01.taxi.dev.yandex.net` - slooow
