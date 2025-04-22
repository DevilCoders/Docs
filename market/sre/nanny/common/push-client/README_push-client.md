## Common push-client configs
[/tmpl/conf/push-client/market_health.yaml](https://a.yandex-team.ru/arc/edit//trunk/arcadia/market/sre/nanny/common/push-client/tmpl/conf/push-client/market_health.yaml) — for sending to a production Logbroker (and testing, prestable and production Logshatter-s) is used in any environment  
[/tmpl/conf/push-client/market_health_pre.yaml](https://a.yandex-team.ru/arc/edit//trunk/arcadia/market/sre/nanny/common/push-client/tmpl/conf/push-client/market_health_pre.yaml) — for sending to a prestable Logbroker (and a development Logshatter) is used only in testing and prestable environments  

### How to use it?
Add a new Container (Runtime Attributes->Instance Spec) with the following command
```
bin/push-client-start.sh
```

### How to configure which log files to send?
A common guide https://wiki.yandex-team.ru/market/development/health/howto/#korotkijjpipeline
variables.tmpl must contain the following code
```
{%- for l in read_plain_text_file("external/push-client.conf") -%}
{{ log_files.append(nginx_log_prefix + "/" + l) }}
{%- endfor -%}
```