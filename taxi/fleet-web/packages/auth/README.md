# @yandex-fleet/auth

[api](https://github.yandex-team.ru/taxi/uservices/blob/develop/services/fleet-ui/docs/yaml)

## How to check permission

1. Add new permissions in [fleet access control permissions config](https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs/edit/FLEET_ACCESS_CONTROL_PERMISSIONS)

There should be at least two permissions — base permission for the feature and inherited permission that will be used to check the feature implementation

Example

```json
"_psat_common": {
  "description": "Common permission for the park satisfaction feature",
  "enabled_for": "all"
},
"psat_send": {
  "description": "Allows sending PSAT results",
  "enabled_for": "all",
  "parent_permission": "_psat_common"
}
```

2. Add inherited permission id to the [Permission enum](src/permission.ts)

Example

```ts
export enum Permission {
  PsatSend = "psat_send",
}
```

3. Check for that permission using either `PermissionBoundary` component or `useHasPermissions` hook

Example

```tsx
import { Permission, PermissionBoundary } from "@yandex-fleet/auth";

<PermissionBoundary permissions={[Permission.PsatSend]} fallback={null}>
  <PSAT />
</PermissionBoundary>;
```

```ts
import { Permission, useHasPermissions } from "@yandex-fleet/auth";

const hasPermission = useHasPermissions(Permission.PsatSend);
```
