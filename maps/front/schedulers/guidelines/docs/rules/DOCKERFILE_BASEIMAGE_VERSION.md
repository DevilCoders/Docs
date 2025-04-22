# DOCKERFILE_BASEIMAGE_VERSION

Requires the version of the baseimage used in the project to be at least equal to the enforced version (see below).

## Rationale
The base docker image is a foundation for the service and contains not only basic infrastructure for monitorings, logging, etc. It also contains a bunch of useful tools and implements our best-practices, which should be consistent across all our services.

## Solution
Update your base image in Dockerfile. You can find enforced versions [here](https://a.yandex-team.ru/arc_vcs/maps/front/tools/docker-baseimages/versions.json).

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/arc/docker-file.test.ts#L44-51)_
