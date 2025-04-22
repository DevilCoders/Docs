# Core resources

Here we reconcile existing resources: Folder, Network and Subnets.

For now, we can not create Subnets with ipv6 address space via provider-jet-yc. You need request its creation manually
via st/YCLOUD. Example: https://st.yandex-team.ru/YCLOUD-3525

### [External name](https://crossplane.io/docs/v1.5/concepts/managed-resources.html#external-name)

To reconcile existing resources define: `metadata.annotations["crossplane.io/external-name"]`:

Example:

```yaml
metadata:
    annotations:
        crossplane.io/external-name: <resource-id>
```

### Deletion policy

> DeletionPolicy specifies what will happen to the underlying external when this managed resource is deleted - either "Delete" or "Orphan" the external resource.

Set `spec.deletionPolicy=Orphan` if you do not want to delete external resource on k8s resource deletion.

Example:

```yaml
spec:
    deletionPolicy: Orphan
```
