# Terrajet based provider yc

Сборка crossplane провайдера поверх yandex.cloud terraform.

Для генерации используется [terrajet](https://github.com/crossplane-contrib/terrajet)

Репозиторий со сгенерированным
провайдером [provider-jet-yc](https://bb.yandex-team.ru/projects/CROSSPLANE/repos/provider-jet-yc)

## Генерация провайдера

* Для генерации собственного провайдера
  используется [provider-jet-template](https://github.com/crossplane-contrib/provider-jet-template).

* Хороший пошаговый гайд по генерации от команды
  crossplane [generating-a-provider.md](https://github.com/crossplane-contrib/terrajet/blob/main/docs/generating-a-provider.md)
  .

* В случае с yandex-cloud делаем исключения для ресурсов на которых падает генерация
  в [config.go](https://bb.yandex-team.ru/projects/CROSSPLANE/repos/provider-jet-yc/browse/config/provider.go#45).

## Namespaced объекты в terrajet контроллерах

* [Патчим crossplane-runtime](https://github.com/crossplane/crossplane-runtime/pull/314)
* [Обновляем crossplane-runtime через replace в go.mod](https://github.com/vaspahomov/terrajet/commit/6e2101dc18851f5c3804e3658e1e053b65b87ec6)
* [В provider-jet-yc меняем terrajet через replace в go.mod, делаем go mod vendor && make generate && make](https://bb.yandex-team.ru/projects/CROSSPLANE/repos/provider-jet-yc/commits/d013a355e1c788b6e979481f93500e0de7bf8917)

