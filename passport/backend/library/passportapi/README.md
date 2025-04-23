==Описание

Клиент для passport-api

## Генерация моков
```
cd mocks
ya tool mockgen -package passportapi_client -source ../interfaces.go -destination passportapi_mock/passportapi_mock.go
ya tool mockgen -package tvm_mock -source ~/src/a.yandex-team.ru/library/go/yandex/tvm/client.go -destination tvm_mock/tvm_mock.go
```
