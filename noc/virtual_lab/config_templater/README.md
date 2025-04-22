# Config Templater
Small helper for Deploy units

Allows to generate config files using Jinja2 templates
Additional objects passed to the template engine:

## Enrironment
`env`
Just a dict with env variables

## SD
`sd`
Allows to resolve endpoint sets to list of pods
Attributes:
`endpoints` - dict, use endpoint name as key, value is list of pods

## Pod Agent
`pod_agent`
Passes information from Pod Agent API
Attributes:
`pod_attributes` - object with http://localhost:1/pod_attributes data

## Deploy
`deploy`
Allow to query Deploy API
Requires YP OAuth token in `~/.dctl/token` or `DCTL_YP_TOKEN` env var
Attributes:
`endpoints` - dict, use endpoint name as key. Sme as `dctl list endpoint`


## Example
```jinja
port: 1235
cpu: {{ (pod_agent.pod_attributes.resource_requirements.cpu.cpu_limit_millicores / 1024) | round(method="ceil") | int }}
ram: {{ (pod_agent.pod_attributes.resource_requirements.memory.memory_limit_bytes / 2**20) | int }}
work dir: "{{ env["AGENT_WORK_DIR"] }}"
{% if sd.endpoints[env["COORDIDNATOR_ENDPOINT"]] %}
coordinators:
{% for pod in sd.endpoints[env["COORDIDNATOR_ENDPOINT"]] %}
  - {{ pod.fqdn }}
{% endfor %}
{% endif %}
```
