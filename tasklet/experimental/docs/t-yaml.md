# YAML-спецификация тасклетов

## Пример {#example}

```yaml
meta:
    name: dummy_tasklet
    description: "Just a dummy testing tasklet"
    namespace: test-tasklets
    catalog: /library/test
    owner: abc:tasklets
    tracking_label: latest
spec:
    naive_schema:
        input_message: tasklet.api.v2.GenericBinary
        output_message: tasklet.api.v2.GenericBinary

    executor:
        type: binary

    container:
        cpu_limit: 1000
        ram_limit: 100MB
        workdir:
            type: hdd
            space: 100MB
    environment:
        arc_client: true
```

## Meta

В секции `meta` находится описание тасклета.

## Spec

В секции `spec` находится описание билда.
