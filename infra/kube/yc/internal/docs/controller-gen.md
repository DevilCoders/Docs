# Controller gen

Автоматизация написания crossplane контроллеров для yandex.cloud.

## Пример генерации контроллера для vpc.Network

1. Описываем параметры ресурса в
   [gen.go](https://bb.yandex-team.ru/projects/CROSSPLANE/repos/yandex-service-operator/browse/internal/controllerutil/gen.go)
   в функции `GenerateResources()`

   Добавляем описание:
   ```
   "vpc.Network": GenerateResource(&ResourceArgs{
       Name:    "Network",
       SdkPath: "VPC().Network()",
       Package: "vpc",
       Imports: append(defaultImports, vpcImports...),
   }),
   ```

2. Пересобираем генератор
   в [cmd/generator](https://bb.yandex-team.ru/projects/CROSSPLANE/repos/yandex-service-operator/browse/cmd/generator)
   `go build .`

3. Запускаем генератор `./generator`
4. Сгенерированный код контроллера появится
   в [zz_controller.go](https://bb.yandex-team.ru/projects/CROSSPLANE/repos/yandex-service-operator/browse/internal/controller/vpc/network/zz_controller.go)
5. Руками реализуем интерфейс в соседнем
   файле [network.go](https://bb.yandex-team.ru/projects/CROSSPLANE/repos/yandex-service-operator/browse/internal/controller/vpc/network/network.go)

```go
func (c *external) fillGetRequest(cr *v1alpha1.Network, req *pb.GetNetworkRequest) {
// todo: fill GetNetworkRequest
}

func (c *external) fillCreateRequest(cr *v1alpha1.Network, req *pb.CreateNetworkRequest) {
// todo: fill CreateNetworkRequest
}

func (c *external) fillUpdateRequest(cr *v1alpha1.Network, req *pb.UpdateNetworkRequest) {
// todo: fill UpdateNetworkRequest
}

func (c *external) fillDeleteRequest(cr *v1alpha1.Network, req *pb.DeleteNetworkRequest) {
// todo: fill DeleteNetworkRequest
}

func (c *external) makeExternalObservation(cr *v1alpha1.Network, observation *vpc.Network) (managed.ExternalObservation, error) {
// todo: Fill status here
// todo: Late initialize
// todo: Drift detection
return managed.ExternalObservation{}, nil
}
```
