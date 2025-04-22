# Import-credentials tool

Generates [SEDEM secrets config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/staticapi/sedem_config/secrets.yaml).

Validates:
- credentials in YaVault: https://yav.yandex-team.ru/?tags=maps-staticapi-apikey
- ratelimiter configs
    - [maps_core_renderer_staticapi/stable.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_core_renderer_staticapi/stable.yaml)
    - [maps_core_renderer_staticapi/testing.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_core_renderer_staticapi/testing.yaml)
- [staticapi_visual_tests.html](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/staticapi/staticapi_visual_tests.html)

## Authorization in YaVault

### ssg-agent
Tool uses ssh-agent to authorize in YaVault by default.

### OAuth
To authorize by OAuth-token:
1. Get OAuth-token: call `ya vault oauth` or [open link in browser](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982).
2. Call tool with `--oauth TOKEN` param.
