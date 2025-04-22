[BCM2](../README.md) / [Exports](../modules.md) / [base/transport](../modules/base_transport.md) / Transport

# Class: Transport<Options, Params, Request, RawResponse, Response, Stats\>

[base/transport](../modules/base_transport.md).Transport

Базовый класс описание Транспортного слоя

## Type parameters

Name | Type | Default |
:------ | :------ | :------ |
`Options` | [*TransportOptions*](../modules/base_transport.md#transportoptions) | [*TransportOptions*](../modules/base_transport.md#transportoptions) |
`Params` | [*TransportParams*](../modules/base_transport.md#transportparams) | [*TransportParams*](../modules/base_transport.md#transportparams) |
`Request` | [*TransportRequest*](../interfaces/base_transport.transportrequest.md) | [*TransportRequest*](../interfaces/base_transport.transportrequest.md) |
`RawResponse` | [*TransportRawResponse*](../interfaces/base_transport.transportrawresponse.md) | [*TransportRawResponse*](../interfaces/base_transport.transportrawresponse.md) |
`Response` | [*TransportResponse*](../interfaces/base_transport.transportresponse.md) | [*TransportResponse*](../interfaces/base_transport.transportresponse.md) |
`Stats` | [*TransportStats*](../interfaces/base_transport.transportstats.md) | [*TransportStats*](../interfaces/base_transport.transportstats.md) |

## Hierarchy

* [*BaseModel*](base_model.basemodel.md)

  ↳ **Transport**

  ↳↳ [*HttpTransport*](http_transport.httptransport.md)

## Table of contents

### Constructors

- [constructor](base_transport.transport.md#constructor)

### Properties

- [context](base_transport.transport.md#context)
- [options](base_transport.transport.md#options)
- [DEFAULT\_RETRY\_DELAY](base_transport.transport.md#default_retry_delay)

### Methods

- [afterError](base_transport.transport.md#aftererror)
- [afterResponse](base_transport.transport.md#afterresponse)
- [beforeSend](base_transport.transport.md#beforesend)
- [getMaxRetryCount](base_transport.transport.md#getmaxretrycount)
- [prepareParams](base_transport.transport.md#prepareparams)
- [prepareRequest](base_transport.transport.md#preparerequest)
- [prepareResponse](base_transport.transport.md#prepareresponse)
- [request](base_transport.transport.md#request)
- [retryAllowed](base_transport.transport.md#retryallowed)
- [send](base_transport.transport.md#send)
- [connect](base_transport.transport.md#connect)
- [factory](base_transport.transport.md#factory)
- [setup](base_transport.transport.md#setup)

## Constructors

### constructor

\+ **new Transport**<Options, Params, Request, RawResponse, Response, Stats\>(`context`: [*Context*](base_context.context.md)): [*Transport*](base_transport.transport.md)<Options, Params, Request, RawResponse, Response, Stats\>

#### Type parameters:

Name | Type | Default |
:------ | :------ | :------ |
`Options` | *Partial*<{ [key: string]: *any*; `retry`: *number* ; `retryAllowed`: (`error`: Error) => *boolean* ; `retryDelay`: *number* \| [*RetryDelay*](../modules/util_retry.md#retrydelay)  }\> | *Partial*<{ [key: string]: *any*; `retry`: *number* ; `retryAllowed`: (`error`: Error) => *boolean* ; `retryDelay`: *number* \| [*RetryDelay*](../modules/util_retry.md#retrydelay)  }\> |
`Params` | *Partial*<{ [key: string]: *any*; `backend`: *string* ; `retry`: *number* ; `retryAllowed`: (`error`: Error) => *boolean* ; `retryDelay`: *number* \| [*RetryDelay*](../modules/util_retry.md#retrydelay)  }\> | *Partial*<{ [key: string]: *any*; `backend`: *string* ; `retry`: *number* ; `retryAllowed`: (`error`: Error) => *boolean* ; `retryDelay`: *number* \| [*RetryDelay*](../modules/util_retry.md#retrydelay)  }\> |
`Request` | [*TransportRequest*](../interfaces/base_transport.transportrequest.md) | [*TransportRequest*](../interfaces/base_transport.transportrequest.md) |
`RawResponse` | [*TransportRawResponse*](../interfaces/base_transport.transportrawresponse.md) | [*TransportRawResponse*](../interfaces/base_transport.transportrawresponse.md) |
`Response` | [*TransportResponse*](../interfaces/base_transport.transportresponse.md) | [*TransportResponse*](../interfaces/base_transport.transportresponse.md) |
`Stats` | [*TransportStats*](../interfaces/base_transport.transportstats.md) | [*TransportStats*](../interfaces/base_transport.transportstats.md) |

#### Parameters:

Name | Type |
:------ | :------ |
`context` | [*Context*](base_context.context.md) |

**Returns:** [*Transport*](base_transport.transport.md)<Options, Params, Request, RawResponse, Response, Stats\>

Inherited from: [BaseModel](base_model.basemodel.md)

Defined in: lib/lib/bcm2/src/base/model.ts:26

## Properties

### context

• `Readonly` **context**: [*Context*](base_context.context.md)

Inherited from: [BaseModel](base_model.basemodel.md).[context](base_model.basemodel.md#context)

Defined in: lib/lib/bcm2/src/base/model.ts:26

___

### options

• `Readonly` **options**: Options

Настройки

Defined in: lib/lib/bcm2/src/base/transport.ts:101

___

### DEFAULT\_RETRY\_DELAY

▪ `Static` **DEFAULT\_RETRY\_DELAY**: *number*= 100

Defined in: lib/lib/bcm2/src/base/transport.ts:76

## Methods

### afterError

▸ `Protected`**afterError**(`params`: Params, `request`: Request, `stats`: Stats, `error`: Error, `willRetry`: *boolean*): *void*

Хук. Вызывается после ошибок отправки запроса

#### Parameters:

Name | Type |
:------ | :------ |
`params` | Params |
`request` | Request |
`stats` | Stats |
`error` | Error |
`willRetry` | *boolean* |

**Returns:** *void*

Defined in: lib/lib/bcm2/src/base/transport.ts:184

___

### afterResponse

▸ `Protected`**afterResponse**(`params`: Params, `request`: Request, `stats`: Stats, `response`: Response): *void*

Хук. Вызывается после успешного получения ответа

#### Parameters:

Name | Type |
:------ | :------ |
`params` | Params |
`request` | Request |
`stats` | Stats |
`response` | Response |

**Returns:** *void*

Defined in: lib/lib/bcm2/src/base/transport.ts:170

___

### beforeSend

▸ `Protected`**beforeSend**(`params`: Params, `request`: Request, `stats`: Stats): *void*

Хук. Вызывается перед отправкой запроса

#### Parameters:

Name | Type |
:------ | :------ |
`params` | Params |
`request` | Request |
`stats` | Stats |

**Returns:** *void*

Defined in: lib/lib/bcm2/src/base/transport.ts:157

___

### getMaxRetryCount

▸ `Protected`**getMaxRetryCount**(`params`: Params): *number*

Возвращает финальное значение retry

#### Parameters:

Name | Type |
:------ | :------ |
`params` | Params |

**Returns:** *number*

Defined in: lib/lib/bcm2/src/base/transport.ts:207

___

### prepareParams

▸ `Protected`**prepareParams**(`params`: Params): *Promise*<Params\>

Подготовка параметров запроса

#### Parameters:

Name | Type |
:------ | :------ |
`params` | Params |

**Returns:** *Promise*<Params\>

Defined in: lib/lib/bcm2/src/base/transport.ts:109

___

### prepareRequest

▸ `Protected`**prepareRequest**(`params`: Params): *Promise*<Request\>

Подготовка запроса

#### Parameters:

Name | Type |
:------ | :------ |
`params` | Params |

**Returns:** *Promise*<Request\>

Defined in: lib/lib/bcm2/src/base/transport.ts:119

___

### prepareResponse

▸ `Protected`**prepareResponse**(`request`: Request, `response`: RawResponse, `params?`: Params): *Promise*<Response\>

Подготовка ответа

#### Parameters:

Name | Type |
:------ | :------ |
`request` | Request |
`response` | RawResponse |
`params?` | Params |

**Returns:** *Promise*<Response\>

Defined in: lib/lib/bcm2/src/base/transport.ts:131

___

### request

▸ `Protected`**request**(`request`: Request): *Promise*<RawResponse\>

Попытка отправки запроса

#### Parameters:

Name | Type |
:------ | :------ |
`request` | Request |

**Returns:** *Promise*<RawResponse\>

Defined in: lib/lib/bcm2/src/base/transport.ts:146

___

### retryAllowed

▸ `Protected`**retryAllowed**(`params`: Params, `error`: Error): *boolean*

Проверка разрешения на ретрай

#### Parameters:

Name | Type |
:------ | :------ |
`params` | Params |
`error` | Error |

**Returns:** *boolean*

Defined in: lib/lib/bcm2/src/base/transport.ts:196

___

### send

▸ **send**(`params`: Params): *Promise*<Response\>

Отправка запроса

#### Parameters:

Name | Type |
:------ | :------ |
`params` | Params |

**Returns:** *Promise*<Response\>

Defined in: lib/lib/bcm2/src/base/transport.ts:218

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

▸ `Static`**setup**<Current, Options\>(`options`: Options): [*ConcreteTransportClass*](../modules/base_transport.md#concretetransportclass)<Current, Options\>

Настройка транспорта

#### Type parameters:

Name | Type |
:------ | :------ |
`Current` | [*AnyTransport*](../modules/base_transport.md#anytransport)<Options\> |
`Options` | *Partial*<{ [key: string]: *any*; `retry`: *number* ; `retryAllowed`: (`error`: Error) => *boolean* ; `retryDelay`: *number* \| [*RetryDelay*](../modules/util_retry.md#retrydelay)  }\> |

#### Parameters:

Name | Type |
:------ | :------ |
`options` | Options |

**Returns:** [*ConcreteTransportClass*](../modules/base_transport.md#concretetransportclass)<Current, Options\>

Defined in: lib/lib/bcm2/src/base/transport.ts:264
