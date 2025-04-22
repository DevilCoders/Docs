## usage

Generate tickets:

    ./generate tickets

Generate plan for specific abc service:

    ./generate plan_it --abc-services 1465 --cluster sas-test > ./pods.yaml

Apply zero limits for specific service:

    ./generate --no-dry-run apply_it --use-limits --zero-limits --services rtc-instance-resolver-production ./pods.yaml

Generate tickets for specific service with hdd:

    ./generate tickets --abc-services 1465 --storage-class hdd

Generate plan for QYP:

    ./generate plan_it --abc-services 1172 --cluster vla --ignore-approvement --deploy-engines QYP

Generate tickets also for QYP:

    ./generate qyp_tickets --abc-services 1465

## apply guarantee

Upload guarantee:

    ./generate plan_it --cluster sas --abc-services 4349 > plan.yaml
    cat plan.yaml
    ./generate apply_it ./plan.yaml
    ./generate --no-dry-run apply_it ./plan.yaml

Find what's left:

    ./generate apply_it ./plan.yaml 2>&1 | grep "disk spec should be changed" | wc -l
    
## change limits&guarantees manually

    ./generate change_limits  --nannyservices 'alice_begemot_megamind_rc aurora_production_workers_sas' 
    --ssd_limit 60 --hdd_limit 50

Дифф по квотам будет выгружен в отдельный файл, после запуска необходимо закоммитить измененные io_limits.json и abc_quotas.json
Для всех сервисов, перечисленных через пробел, выставляется один и тот же лимит. Аргументы ssd_limit и hdd_limit не обязательны,
но хотя бы один из лимитов должен быть выставлен. Гарантия и квота для HDD выставляется с учетом коэффициента оверкоммита.


## generate QYP limits&guarantees

1. Удаляем yp_stat.tmp
2. Выполняем команду, которая соберет актуальные данные по подам вм и модифицирует io_limits.json

       ./generate compute_qyp_limits
3. Коммиитм io_limits.json

## links
* https://wiki.yandex-team.ru/users/glebskvortsov/iossdreadlimits/#instrukcija
* https://wiki.yandex-team.ru/users/dldmitry/iolimitnotes/
* https://st.yandex-team.ru/RTCRESOURCES/
* https://yav.yandex-team.ru/secret/sec-01e08j0ct8xhj3bj1r9m6jq16j/explore/versions

## tokens
* YP: ~/.yp/token, https://wiki.yandex-team.ru/yp/accesscontrol/
* ST: ~/.st/token, https://wiki.yandex-team.ru/tracker/api/
* NANNY: ~/.nanny/token, https://nanny.yandex-team.ru/ui/#/oauth/
* OK: ~/.ok/token, https://wiki.yandex-team.ru/Intranet/OK/private-api/
