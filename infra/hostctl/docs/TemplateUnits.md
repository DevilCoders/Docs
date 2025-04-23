# Templated units

Hostctl supports management of templated systemd units (SystemSerivce and TimerJob).

Templated units are monitored and managed as single hostctl unit.

To make unit templated there are two requirements:
* hostctl unit name must end with '@' (should be the same as systemd-unit@.service and/or systemd-unit@.timer without unit type suffix)
* spec.template.instances must have at least one instance defined

## Example

    vars:
      - name: stage
        match:
          - exp: "default()"
            val: "stable"
      - name: version
        match:
          - exp: "default()"
            val: "7845240"
    ---
    meta:
      name: yandex-sol-rtc@
      version: "{version}"
      kind: SystemService
      annotations:
        stage: "{stage}"
    spec:
      packages:
        - name: yandex-sol-rtc
          version: "{version}"
      template:
        instances:
          - ttyS0
          - ttyS1

In this example hostctl will manage yandex-sol-rtc@ttyS0.service and yandex-sol-rtc@ttyS1.service systemd units as one. Failure in any managed instance will be reported as whole hostctl unit failure.
