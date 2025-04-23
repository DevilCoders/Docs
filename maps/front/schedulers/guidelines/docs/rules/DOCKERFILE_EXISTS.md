# DOCKERFILE_EXISTS

Requires a Dockerfile to be present in the service's repository.

## Rationale
To make our services infrastructure consistent, docker was chosen as a way to transport the code to the servers.
That's why a Dockerfile is required for all of our services.

## Solution
Add `Dockerfile` into project repository's root folder.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/arc/docker-file.test.ts#L30-32)_
