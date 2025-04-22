# ABC_SERVICE_NAME_PREFIX

Requires `maps-front-` prefix for ABC service slug.

## Rationale
Prefix `maps-front` is used to separate our team services from others. The same prefix is used in various internal services: ABC, Awacs, and etc. It makes it possible to connect all this entities between different systems.

## Solution
ABC slug can't be changed, so you should create a new one:
1. Rename current ABC service by adding "[OLD]" prefix to its name.
1. Create a new ABC service with a correct slug.
1. Copy all collaborators from the old service to the new one.
1. Move all contacts from the old ABC service to the new.
1. Change ABC service in the ACL of all projects (Deploy, AWACS, etc).
1. Transfer all firewall rules in [Puncher](https://puncher.yandex-team.ru/).
1. Remove old ABC service.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/abc/service-name.test.ts#L22-24)_
