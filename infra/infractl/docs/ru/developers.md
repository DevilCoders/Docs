# Внутренняя документация для разработчиков

## Код

* [infractl][infractl]
* [protoc_gen_crd][protoc_gen_crd]

## Домены

Prestable:

* https://dev-k.yandex-team.ru — k8s API server
* https://webhooks.dev-k.yandex-team.ru — validation webhooks

Production:

* https://k.yandex-team.ru — k8s API server
* https://infractl-wh.deploy.yandex-team.ru — validation webhooks

## Сервисы

Prestable:

* [pre_infractl_kube_apiserver](https://nanny.yandex-team.ru/ui/#/services/catalog/pre_infractl_kube_apiserver)
* [pre_infractl_k8s_webhooks](https://nanny.yandex-team.ru/ui/#/services/catalog/pre_infractl_k8s_webhooks)
* [authctl-testing](https://deploy.yandex-team.ru/stages/authctl-testing)
* [deployctl-testing](https://deploy.yandex-team.ru/stages/deployctl-testing)

Production:

* [prod_infractl_kube_apiserver](https://adm-nanny.yandex-team.ru/ui/#/services/catalog/prod_infractl_kube_apiserver)
* [prod_infractl_k8s_webhooks](https://nanny.yandex-team.ru/ui/#/services/catalog/prod_infractl_k8s_webhooks)
* [rolesctl-prod](https://deploy.yandex-team.ru/stages/rolesctl-prod)
* [deployctl-prod-xdc](https://deploy.yandex-team.ru/stages/deployctl-prod-xdc)
* [runtimectl-prod-xdc](https://deploy.yandex-team.ru/stages/runtimectl-prod-xdc)

## Типы данных

В качестве базового типа данных спек мы используем Protobuf.
Для использования их в k8s у нас есть protoc-плагин [protoc_gen_crd][protoc_gen_crd], транслирующий protobuf в YAML-спеку OpenAPIv3.

Для использования такой спеки в качестве CRD в k8s надо объявить два параллельных пакета примерно такой структуры:

    api
    \_ proto_v1 (PROTO_LIBRARY)
       \_ spec.proto:
             import "library/go/k8s/protoc_gen_crd/proto/crd.proto";

             message Spec {
                 // your fields
             }

             message Status {
                 // your fields
             }

             message MyCrdKind {
                 option (protoc_gen_crd.k8s_crd) = {
                     api_group: "my-api.yandex-team.ru",
                     kind: "MyCrdKind",
                     plural: "mycrdkinds",
                     singular: "mycrdkind",
                };

                Spec spec = 1;
                Status status = 2;
            }
       \_ ya.make:
            PROTO_LIBRARY()
            ...
            INCLUDE(${ARCADIA_ROOT}/library/go/k8s/protoc_gen_crd/build.inc)
            INCLUDE(${ARCADIA_ROOT}/yt/yt/orm/go/codegen/proto-comments/build.inc)
            INCLUDE(${ARCADIA_ROOT}/yp/go/protoc-gen-deepcopy/build.inc)
    \_ v1 (GO_LIBRARY)
      \_ spec.go:
            type MyCrdKind struct {
                metav1.TypeMeta   `json:",inline"`
                metav1.ObjectMeta `json:"metadata,omitempty"`

                Spec   *proto_v1.Spec   `json:"spec,omitempty"`
                Status *proto_v1.Status `json:"status,omitempty"`
            }

В коде, работающим с CRD, надо будет использовать тип `v1.MyCrdKind` и все содержащиеся в нём типы, а непосредственно message `proto_v1.MyCrdKind` будет использоваться только как маркер для генерации OpenAPI.

## Контроллеры

Инструкции по сборке каждого отдельного контроллера описаны в соответствующем README.md в корне контроллера.

### Roles

[Код](https://a.yandex-team.ru/arc_vcs/infra/infractl/controllers/roles)

Автоматически выдаёт пользователям роли при создании нового namespace в k8s.

### Deploystage

[Код](https://a.yandex-team.ru/arc_vcs/infra/infractl/controllers/deploy)

Контроллер, перекладывающий спеки стейджей из k8s в Deploy.

### Runtime

[Код](https://a.yandex-team.ru/arc_vcs/infra/infractl/controllers/runtime)

Контроллер, собирающий спеку Deploystage из упрощённой спеки.

### Webhooks

[Код](https://a.yandex-team.ru/arc_vcs/infra/infractl/webhooks)

Хуки, валидирующие пользовательский ввод при заливке в k8s.

## Локальная разработка и тестирование.

### Поднятие minikube

```
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo cp minikube-linux-amd64 /usr/local/bin/minikube
minikube start
```

### Применение CRD

Из каталога соответствующего контроллера:
```
ya make --add-result .go --add-result .yaml --replace-result api/proto_v1/
kubectl create -f api/proto_v1/*.crd.yaml
```

## Обновление компонентов

### Контроллеры

Контроллеры (пока что) собираются при помощи `ya package --tar --sandbox --upload build.json` из каталога контроллера.
После этого обновляется соответствующий слой в сервисе контроллера.

CRD заливается аналогично локальной разработке:

```
ya make --add-result .go --add-result .yaml --replace-result api/proto_v1/
kubectl create -f api/proto_v1/*.crd.yaml
```

Перед заливкой всегда необходимо проверять, что в `~/.kube/config` выбран правильный current-context.

### ya tool infractl

Собирается таск BUILD_ARCADIA_PROJECT_FOR_ALL в Sandbox, с таргетом `infra/infractl/cli/infractl`.
Поддерживаемые платформы сейчас: `linux, darwin, win32`.

Пример таска: https://sandbox.yandex-team.ru/task/1260210162/view

После сборки обновляется ID сборочного таска в yatool: https://a.yandex-team.ru/arc_vcs/build/ya.conf.json?rev=r9291449#L7321

### ya tool kubectl

Положить kubectl в аркадию сложно, поэтому собирается он так:

```bash
git clone https://github.com/kubernetes/kubernetes/
cd kubernetes/cmd/kubectl
GOOS=linux GOARCH=amd64 ya tool go build
tar czf kubectl-linux-amd64.tar.gz kubectl
GOOS=windows GOARCH=amd64 ya tool go build
tar czf kubectl-windows-amd64.tar.gz kubectl.exe
GOOS=darwin GOARCH=amd64 ya tool go build
tar czf kubectl-darwin-amd64.tar.gz kubectl

ya upload kubectl-darwin-amd64.tar.gz -T ARCADIA_PROJECT_TGZ -a darwin -A platform=darwin -d 'kubectl for darwin'
ya upload kubectl-linux-amd64.tar.gz -T ARCADIA_PROJECT_TGZ -a linux -A platform=linux -d 'kubectl for linux'
ya upload kubectl-windows.tar.gz -T ARCADIA_PROJECT_TGZ -a win_nt -A platform=win32 -d 'kubectl for windows'

cd ~/workspace/arc/junk/torkve/build_for_all
ya make
vim input.example.json  # указать полученные resource_ids
./build_for_all run --sandbox --input "$(cat input.example.json)" BuildForAll
```

### Создание кастомных CRD по запросу пользователя
После того как пользователь выполнит все необходимые [пререквизиты](https://docs.yandex-team.ru/infractl/guides#cutom-crd-creation) для создания кастомного CRD, делаем следующее:

1. Подтвердить роль, запрошенную пользователем в IDM.
2. Подтвердить дырку, запрошенную пользователем в Панчере.
3. Создать в k8s CRD, полученный от пользователя.
4. Создать в k8s [роль](https://a.yandex-team.ru/arc_vcs/infra/infractl/manifests/custom-crd-admin-role.yaml) и [биндинг](https://a.yandex-team.ru/arc_vcs/infra/infractl/manifests/custom-crd-admin-binding.yaml) для соответствующего CRD, подставив нужное имя ресурса.


[infractl]: https://a.yandex-team.ru/arc_vcs/infra/infractl/
[protoc_gen_crd]: https://a.yandex-team.ru/arc_vcs/library/go/k8s/protoc_gen_crd/
