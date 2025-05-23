Авторизация операций возникает в двух видах сервисов: в сервисе, управляющем сущностями, и в сервисе операций.

```proto
service ExampleService {
  rpc ListOperations (ListExampleOperationsRequest) returns (ListExampleOperationsResponse)
}

message ListExampleOperationsRequest {
  string resource_id = 1;
}
```

```proto
service OperationService {
  rpc Get (GetOperationRequest) returns (operation.Operation)
  rpc Cancel (CancelOperationRequest) returns (operation.Operation)
}

message GetOperationRequest {
  string operation_id = 1;
}

message CancelOperationRequest {
  string operation_id = 1;
}
```

Во всех случаях в качестве ресурса авторизации используется сам ресурс, с которым связана операция. В качестве
permission:
- `<service>.<resource>.get` в случае `ListOperations`/`Get` 
- тот permission, который использовался для создания операции, в случае `Cancel` (например, `<service>.<resource>.create`,
  если это была операция создания нового ресурса или `<service>.<resource>.delete` для операций удаления).

{% note info %}

Permission `<service>.<resource>.get`, а не отдельный permission, выбран потому, что при чтении операции в ее метаданных
и так уже доступны атрибуты ресурса. Это немного сужает возможности по ограничению доступа к сущностям: для создания
ресурсов нужно иметь на контейнере роль, позволяющую делать и чтение ресурсов в этом контейнере, т.е. нельзя выдать права
исключительно на создание новых ресурсов и при этом получать доступ к статусу операции создания ресурса. В будущем несложно
будет разделить эти два действия и сделать отдельный permission для получения операции, если появится такая необходимость.

Аналогичные рассуждения работают и для отмены операций: при необходимости в будущем можно будет выделить отмену в отдельный
permission.

{% endnote %}

Авторизация получения и отмены операции _удаления ресурса_ или _создания ресурса верхнего уровня_ должна быть всегда
успешна для ее инициатора, т.е. еще до проверки прав сервис должен проверить, не является ли субъект, получающий доступ к
операции, ее инициатором.

{% note info %}

Такая схема авторизации операций сделана из-за наличия двух случаев, когда стандартная авторизация только на ресурс может
быть неудобна.

При авторизации создания ресурсов верхнего уровня (например, облаков) возникает ситуация, что авторизовать создателя на
новом ресурсе невозможно: ресурс может быть уже создан в статусе `CREATING`, но права на него еще не успели быть назначены,
т.к. назначаются с помощью асинхронного вызова в сторонний сервис.

При удалении ресурса инициатор удаления мог иметь права, выданные только на сам ресурс (а не на его контейнер, к
примеру), поэтому после завершения удаления авторизация на этот ресурс станет неуспешной и пользователь не сможет
узнать статус операции удаления.

Оборотной стороной такого подхода является то, что у инициатора нельзя забрать права на отмену таких операций. Мы считаем
эту особенность некритичной с точки зрения безопасности, т.к. в момент создания ресурса у инициатора уже была вся
информация, которая возвращается в операции (либо он передал ее в серис сам в метод создания ресурса, либо имел к ней
доступ). При изменении ресурса доступ к измененной информации инициатор не получает.

{% endnote %}
