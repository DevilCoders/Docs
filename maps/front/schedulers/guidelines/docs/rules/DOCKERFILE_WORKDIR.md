# DOCKERFILE_WORKDIR

Requires `/usr/local/app` to be used as `WORKDIR`.

## Rationale
The DevOps team should have an uniform way to find the built application in a docker container. For that reason it is required to place your built application in `/usr/local/app`.

## Solution
Make sure that you use the `WORKDIR /usr/local/app` directive in your Dockerfile and that your built application is placed in `/usr/local/app`.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/arc/docker-file.test.ts#L80-85)_
