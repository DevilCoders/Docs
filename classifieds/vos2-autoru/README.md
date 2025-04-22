# Vertical Offers Service (VOS)

See https://wiki.yandex-team.ru/vertis/vos/

## Requirements
  - java 8
  - Apache Maven
  - Docker (for tests)
  - jpegoptim
  - imagemagick

## Deploy to testing

From `master` branch you run one of these TeamCity jobs (depending on what component you need), build arfifact gonna be deployed to `testing` enviroment after successfull build.
1. Build [vos2-autoru-api](https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=Vos2_autoru_Vos2autoruApiDockerRelease)
2. Build [vos2-autoru-scheduler](https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=Vos2_autoru_Vos2autoruSchedulerDockerRelease) (some stages are deprecated and replaced by stages from vos2-autoru-ydb-workers) 
3. Build [vos2-autoru-ydb-workers](https://t.vertis.yandex-team.ru/buildConfiguration/Vos2_autoru_Vos2autoruYdbWorkersDocker?mode=builds#all-projects) (replaces some stages from vos2-autoru-scheduler)

## git-hooks
To enable git hooks you need to cd to `<project directory>/scripts/hooks` and run
`chmod +x setup-git-hooks.sh && ./setup-git-hooks.sh`

If you need to update hooks, just run `./setup-git-hooks.sh` after pulling changes from github.

## Code format
`make fmt`

## Local tests for schedulers
Disable experimental features in docker to avoid [testcontainers stoped working](https://jira.atlassian.com/browse/BCLOUD-17236) issue
![Docker properties window](doc/img/docker_experimental.png)

