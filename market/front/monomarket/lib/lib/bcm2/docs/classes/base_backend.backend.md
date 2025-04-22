[BCM2](../README.md) / [Exports](../modules.md) / [base/backend](../modules/base_backend.md) / Backend

# Class: Backend<T\>

[base/backend](../modules/base_backend.md).Backend

Базовый класс Бекендов.

## Type parameters

Name | Type |
:------ | :------ |
`T` | [*Transport*](base_transport.transport.md) |

## Hierarchy

* [*BaseModel*](base_model.basemodel.md)

  ↳ **Backend**

## Table of contents

### Constructors

- [constructor](base_backend.backend.md#constructor)

### Properties

- [context](base_backend.backend.md#context)
- [transport](base_backend.backend.md#transport)
- [backendName](base_backend.backend.md#backendname)
- [options](base_backend.backend.md#options)

### Accessors

- [name](base_backend.backend.md#name)

### Methods

- [fetch](base_backend.backend.md#fetch)
- [prepareRequest](base_backend.backend.md#preparerequest)
- [prepareResponse](base_backend.backend.md#prepareresponse)
- [connect](base_backend.backend.md#connect)
- [factory](base_backend.backend.md#factory)
- [setup](base_backend.backend.md#setup)

## Constructors

### constructor

\+ **new Backend**<T\>(`context`: [*Context*](base_context.context.md)): [*Backend*](base_backend.backend.md)<T\>

#### Type parameters:

Name | Type |
:------ | :------ |
`T` | [*Transport*](base_transport.transport.md)<Partial<{ [key: string]: *any*; `retry`: *number* ; `retryAllowed`: (`error`: Error) => *boolean* ; `retryDelay`: *number* \| [*RetryDelay*](../modules/util_retry.md#retrydelay)  }\>, Partial<{ [key: string]: *any*; `backend`: *string* ; `retry`: *number* ; `retryAllowed`: (`error`: Error) => *boolean* ; `retryDelay`: *number* \| [*RetryDelay*](../modules/util_retry.md#retrydelay)  }\>, [*TransportRequest*](../interfaces/base_transport.transportrequest.md), [*TransportRawResponse*](../interfaces/base_transport.transportrawresponse.md), [*TransportResponse*](../interfaces/base_transport.transportresponse.md), [*TransportStats*](../interfaces/base_transport.transportstats.md), T\> |

#### Parameters:

Name | Type |
:------ | :------ |
`context` | [*Context*](base_context.context.md) |

**Returns:** [*Backend*](base_backend.backend.md)<T\>

Inherited from: [BaseModel](base_model.basemodel.md)

Defined in: lib/lib/bcm2/src/base/model.ts:26

## Properties

### context

• `Readonly` **context**: [*Context*](base_context.context.md)

Inherited from: [BaseModel](base_model.basemodel.md).[context](base_model.basemodel.md#context)

Defined in: lib/lib/bcm2/src/base/model.ts:26

___

### transport

• `Readonly` **transport**: T

Defined in: lib/lib/bcm2/src/base/backend.ts:31

___

### backendName

▪ `Static` **backendName**: *string*

Defined in: lib/lib/bcm2/src/base/backend.ts:35

___

### options

▪ `Static` **options**: *Partial*<{ [key: string]: *any*; `retry`: *number* ; `retryAllowed`: (`error`: Error) => *boolean* ; `retryDelay`: *number* \| [*RetryDelay*](../modules/util_retry.md#retrydelay)  }\>

Defined in: lib/lib/bcm2/src/base/backend.ts:33

## Accessors

### name

• get **name**(): *string*

название бекенда

**Returns:** *string*

Defined in: lib/lib/bcm2/src/base/backend.ts:41

## Methods

### fetch

▸ **fetch**(`params`: [*ExtractTransportParams*](../modules/base_transport.md#extracttransportparams)<T\>): *Promise*<any\>

Отправка запроса в бекенд

#### Parameters:

Name | Type |
:------ | :------ |
`params` | [*ExtractTransportParams*](../modules/base_transport.md#extracttransportparams)<T\> |

**Returns:** *Promise*<any\>

Defined in: lib/lib/bcm2/src/base/backend.ts:73

___

### prepareRequest

▸ **prepareRequest**(`params`: [*ExtractTransportParams*](../modules/base_transport.md#extracttransportparams)<T\>): *Promise*<[*ExtractTransportParams*](../modules/base_transport.md#extracttransportparams)<T\>\>

Подготовка запроса

#### Parameters:

Name | Type |
:------ | :------ |
`params` | [*ExtractTransportParams*](../modules/base_transport.md#extracttransportparams)<T\> |

**Returns:** *Promise*<[*ExtractTransportParams*](../modules/base_transport.md#extracttransportparams)<T\>\>

Defined in: lib/lib/bcm2/src/base/backend.ts:50

___

### prepareResponse

▸ **prepareResponse**(`response`: [*ExtractTransportResponse*](../modules/base_transport.md#extracttransportresponse)<T\>, `params`: [*ExtractTransportParams*](../modules/base_transport.md#extracttransportparams)<T\>): *Promise*<any\>

Подготовка ответа

#### Parameters:

Name | Type |
:------ | :------ |
`response` | [*ExtractTransportResponse*](../modules/base_transport.md#extracttransportresponse)<T\> |
`params` | [*ExtractTransportParams*](../modules/base_transport.md#extracttransportparams)<T\> |

**Returns:** *Promise*<any\>

Defined in: lib/lib/bcm2/src/base/backend.ts:60

___

### connect

▸ `Static`**connect**<Current, I\>(`injection`: I): [*ConnectedClass*](../modules/base_model.md#connectedclass)<Current, I\>

Настройка зависимостей

#### Type parameters:

Name | Type |
:------ | :------ |
`Current` | *typeof* [*BaseModel*](base_model.basemodel.md) |
`I` | [*Injection*](../interfaces/base_model.injection.md) |

#### Parameters:

Name | Type |
:------ | :------ |
`injection` | I |

**Returns:** [*ConnectedClass*](../modules/base_model.md#connectedclass)<Current, I\>

Inherited from: [BaseModel](base_model.basemodel.md)

Defined in: lib/lib/bcm2/src/base/model.ts:68

___

### factory

▸ `Static`**factory**<Current\>(`context`: [*Context*](base_context.context.md)): *InstanceType*<Current\>

Фабрика для создания/получения инстанса связанного с контекстом

#### Type parameters:

Name | Type |
:------ | :------ |
`Current` | *typeof* [*BaseModel*](base_model.basemodel.md) |

#### Parameters:

Name | Type |
:------ | :------ |
`context` | [*Context*](base_context.context.md) |

**Returns:** *InstanceType*<Current\>

Inherited from: [BaseModel](base_model.basemodel.md)

Defined in: lib/lib/bcm2/src/base/model.ts:42

___

### setup

▸ `Static`**setup**<T, O, Current\>(`TransportClass`: T, `backendName`: *string*, `options?`: O): [*SetupBackend*](../modules/base_backend.md#setupbackend)<Current, T, O\>

Настройка бекенда. Подключение и настройка транспортного слоя.

#### Type parameters:

Name | Type |
:------ | :------ |
`T` | [*AnyTransport*](../modules/base_transport.md#anytransport)<O\> |
`O` | *Partial*<{ [key: string]: *any*; `retry`: *number* ; `retryAllowed`: (`error`: Error) => *boolean* ; `retryDelay`: *number* \| [*RetryDelay*](../modules/util_retry.md#retrydelay)  }\> |
`Current` | [*AnyBackend*](../modules/base_backend.md#anybackend)<T, O\> |

#### Parameters:

Name | Type |
:------ | :------ |
`TransportClass` | T |
`backendName` | *string* |
`options?` | O |

**Returns:** [*SetupBackend*](../modules/base_backend.md#setupbackend)<Current, T, O\>

Defined in: lib/lib/bcm2/src/base/backend.ts:86
