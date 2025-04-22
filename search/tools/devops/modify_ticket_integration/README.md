# modify_ticket_integration

A tool for mass ticket integration setting (for a pack of services).

Initially written by Anton Zvonarev <shotinleg@yandex-team.ru> and
enhanced by Mikhail Veltishchev <mvel@yandex-team.ru>

# Examples

## Print ticket integration settings for all services matching `production_balancer` string in name
```bash
./modify_ticket_integration -a print -s production_balancer
```

## Add new rule to service
```bash
./modify_ticket_integration -a add -s production_balancer --props 'queue_id:L7_BALANCER,sandbox_task_type:BUILD_BALANCER_CONFIGS_L7,sandbox_resource_type:BALANCER_CONFIGS_BUNDLE,ticket_priority:NORMAL,responsibles:mvel;dmitryno'
```

## Remove all rules from service `service_name` with `queue_id == L7_BALANCER`
```bash
./modify_ticket_integration -a del -s production_balancer --filter 'queue_id:L7_BALANCER'
```

## Remove all rules from service `service_name` with `queue_id == L7_BALANCER` except rules with `sandbox_task_type == BUILD_BALANCER_BINARY`
```bash
./modify_ticket_integration -a del -s production_balancer --filter 'queue_id:L7_BALANCER' --exclude-filter 'sandbox_task_type:BUILD_BALANCER_BINARY'
```

## Set all rules of service `service_name` field `queue_id = QUEUE2`
```bash
./modify_ticket_integration -a edit -s service_name -p 'queue_id:QUEUE2'
```
Both `--filter` and `--exclude-filter` may be applied together for `edit` and `print` command also.
