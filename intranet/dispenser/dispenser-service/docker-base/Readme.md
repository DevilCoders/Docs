<H2> How to update base image </H2>

1. Change docker-base/Dockerfile, commit to branch 
2. Clone task `https://sandbox.yandex-team.ru/task/302198735` - change:
    * `Git parameters -> branch` to checkout changes 
    * `Registry parameters -> Tags to publish image with` to update version
3. Run task -> wait for sucessfull complete
4. Update `FROM registry.yandex.net/dispenser/dispenser-base:1` in Dockerfiles to new version 