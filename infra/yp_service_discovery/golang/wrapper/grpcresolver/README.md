gRPC резолвер поверх YP Service Discovery
=========================================

### Логирование
Логирование осуществляется штатными средствами gRPC.

### Для желающих балансер
Для реализации кастомной логики балансера (e.g. ходить в текущий ДЦ с фоллбеком), резолвер для каждого адреса устанавливает разнообразный набор аттрибутов:
  - `AddressCluster` вернет кластер, вернувший этот адрес
  - `AddressID` - его endpoint id
  - `AddressLabels` - пользовательские лейблы

О самой балансировке в gRPC можно почитать в офф. документации: [Load Balancing in gRPC](https://github.com/grpc/grpc/blob/master/doc/load-balancing.md)

### Не простые жизненные ситуации

  - Service discovery вернул пустой список адресов для всех требуемых ДЦ:
    * если не выставлена опция `WithEmptyAdressList`, то резолвер НЕ очищает список адресов для gRPC коннекта и пробует еще раз через `resolver rate` секунд
  - Service discovery пофейлил резолвинг endpoint set по всех требуемых ДЦ:
    * резолвер НЕ очищает список адресов для gRPC коннекта
    * с экспоненциальным бэкоффом (от 1s до `resolver rate`) пробуем еще

Частичная не возможность отрезолвить адреса (e.g. пофейлился только один ДЦ из двух) считается штатной ситуацией и никаких доп. действий не производится.

### Полезное чтиво
  - [Godoc](http://godoc.yandex-team.ru/pkg/a.yandex-team.ru/infra/yp_service_discovery/golang/wrapper/grpcresolver)
  - [YP Service Discovery](https://wiki.yandex-team.ru/yp/discovery/)
  - [gRPC Name Resolution](https://github.com/grpc/grpc/blob/master/doc/naming.md)
