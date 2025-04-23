# Пакет Танкера в Балансе

## Сборка на testing
Выполняется в [CI Аркадии](https://a.yandex-team.ru/projects/balance/ci/actions/launches?dir=billing%2Ffrontend%2Ftanker&id=release-testing-flow)

Сборка использует docker-образ img-build-tanker, версия которого указана в [a.yaml](./a.yaml) файле. 
Чтобы собрать новый образ, выполнить (указать новую версию)
```(bash)
docker build . -t img-build-tanker
docker tag img-build-tanker registry.yandex.net/billing/frontend/prepare-tanker:0.0.XXX
docker push registry.yandex.net/billing/frontend/prepare-tanker:0.0.XXX
```