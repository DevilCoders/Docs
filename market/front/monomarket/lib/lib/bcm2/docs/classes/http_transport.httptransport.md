[BCM2](../README.md) / [Exports](../modules.md) / [http/transport](../modules/http_transport.md) / HttpTransport

# Class: HttpTransport

[http/transport](../modules/http_transport.md).HttpTransport

Транспортный слой для http-запросов.

## Hierarchy

* [*Transport*](base_transport.transport.md)<[*HttpTransportOptions*](../modules/http_transport_types.md#httptransportoptions), [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams), [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest), [*HttpTransportRawResponse*](../modules/http_transport_types.md#httptransportrawresponse), [*HttpTransportResponse*](../modules/http_transport_types.md#httptransportresponse), [*TransportStats*](../interfaces/base_transport.transportstats.md)\>

  ↳ **HttpTransport**

## Table of contents

### Constructors

- [constructor](http_transport.httptransport.md#constructor)

### Properties

- [context](http_transport.httptransport.md#context)
- [options](http_transport.httptransport.md#options)
- [DEFAULT\_RETRY\_DELAY](http_transport.httptransport.md#default_retry_delay)

### Methods

- [afterError](http_transport.httptransport.md#aftererror)
- [afterResponse](http_transport.httptransport.md#afterresponse)
- [beforeSend](http_transport.httptransport.md#beforesend)
- [encodeRequestBody](http_transport.httptransport.md#encoderequestbody)
- [getMaxRetryCount](http_transport.httptransport.md#getmaxretrycount)
- [parseResponseBody](http_transport.httptransport.md#parseresponsebody)
- [prepareParams](http_transport.httptransport.md#prepareparams)
- [prepareRequest](http_transport.httptransport.md#preparerequest)
- [prepareResponse](http_transport.httptransport.md#prepareresponse)
- [request](http_transport.httptransport.md#request)
- [retryAllowed](http_transport.httptransport.md#retryallowed)
- [send](http_transport.httptransport.md#send)
- [agent](http_transport.httptransport.md#agent)
- [connect](http_transport.httptransport.md#connect)
- [factory](http_transport.httptransport.md#factory)
- [prepareStream](http_transport.httptransport.md#preparestream)
- [setup](http_transport.httptransport.md#setup)

## Constructors

### constructor

\+ **new HttpTransport**(`context`: [*Context*](base_context.context.md)): [*HttpTransport*](http_transport.httptransport.md)

#### Parameters:

Name | Type |
:------ | :------ |
`context` | [*Context*](base_context.context.md) |

**Returns:** [*HttpTransport*](http_transport.httptransport.md)

Inherited from: [Transport](base_transport.transport.md)

Defined in: lib/lib/bcm2/src/base/model.ts:26

## Properties

### context

• `Readonly` **context**: [*Context*](base_context.context.md)

Inherited from: [Transport](base_transport.transport.md).[context](base_transport.transport.md#context)

Defined in: lib/lib/bcm2/src/base/model.ts:26

___

### options

• `Readonly` **options**: [*HttpTransportOptions*](../modules/http_transport_types.md#httptransportoptions)

Настройки

Inherited from: [Transport](base_transport.transport.md).[options](base_transport.transport.md#options)

Defined in: lib/lib/bcm2/src/base/transport.ts:101

___

### DEFAULT\_RETRY\_DELAY

▪ `Static` **DEFAULT\_RETRY\_DELAY**: *number*= 100

Inherited from: [Transport](base_transport.transport.md).[DEFAULT_RETRY_DELAY](base_transport.transport.md#default_retry_delay)

Defined in: lib/lib/bcm2/src/base/transport.ts:76

## Methods

### afterError

▸ `Protected`**afterError**(`params`: [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams), `request`: [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest), `stats`: [*TransportStats*](../interfaces/base_transport.transportstats.md), `error`: Error, `willRetry`: *boolean*): *void*

Хук. Вызывается после ошибок отправки запроса

#### Parameters:

Name | Type |
:------ | :------ |
`params` | [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams) |
`request` | [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest) |
`stats` | [*TransportStats*](../interfaces/base_transport.transportstats.md) |
`error` | Error |
`willRetry` | *boolean* |

**Returns:** *void*

Inherited from: [Transport](base_transport.transport.md)

Defined in: lib/lib/bcm2/src/base/transport.ts:184

___

### afterResponse

▸ `Protected`**afterResponse**(`params`: [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams), `request`: [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest), `stats`: [*TransportStats*](../interfaces/base_transport.transportstats.md), `response`: [*HttpTransportResponse*](../modules/http_transport_types.md#httptransportresponse)): *void*

Хук. Вызывается после успешного получения ответа

#### Parameters:

Name | Type |
:------ | :------ |
`params` | [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams) |
`request` | [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest) |
`stats` | [*TransportStats*](../interfaces/base_transport.transportstats.md) |
`response` | [*HttpTransportResponse*](../modules/http_transport_types.md#httptransportresponse) |

**Returns:** *void*

Inherited from: [Transport](base_transport.transport.md)

Defined in: lib/lib/bcm2/src/base/transport.ts:170

___

### beforeSend

▸ `Protected`**beforeSend**(`params`: [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams), `request`: [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest), `stats`: [*TransportStats*](../interfaces/base_transport.transportstats.md)): *void*

Хук. Вызывается перед отправкой запроса

#### Parameters:

Name | Type |
:------ | :------ |
`params` | [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams) |
`request` | [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest) |
`stats` | [*TransportStats*](../interfaces/base_transport.transportstats.md) |

**Returns:** *void*

Inherited from: [Transport](base_transport.transport.md)

Defined in: lib/lib/bcm2/src/base/transport.ts:157

___

### encodeRequestBody

▸ `Protected`**encodeRequestBody**(`params`: [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams)): *Promise*<[*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams)\>

Сериализация тела запроса.

#### Parameters:

Name | Type |
:------ | :------ |
`params` | [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams) |

**Returns:** *Promise*<[*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams)\>

Defined in: lib/lib/bcm2/src/http/transport.ts:235

___

### getMaxRetryCount

▸ `Protected`**getMaxRetryCount**(`params`: [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams)): *number*

Возвращает финальное значение retry

#### Parameters:

Name | Type |
:------ | :------ |
`params` | [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams) |

**Returns:** *number*

Inherited from: [Transport](base_transport.transport.md)

Defined in: lib/lib/bcm2/src/base/transport.ts:207

___

### parseResponseBody

▸ `Protected`**parseResponseBody**(`body`: *Buffer*, `params`: [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams)): *Promise*<[*HttpTransportResponseBody*](../modules/http_transport_types.md#httptransportresponsebody)\>

Десериализация тела ответа

#### Parameters:

Name | Type |
:------ | :------ |
`body` | *Buffer* |
`params` | [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams) |

**Returns:** *Promise*<[*HttpTransportResponseBody*](../modules/http_transport_types.md#httptransportresponsebody)\>

Defined in: lib/lib/bcm2/src/http/transport.ts:286

___

### prepareParams

▸ `Protected`**prepareParams**(`params`: [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams)): *Promise*<[*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams)\>

Подготовка параметров запроса

#### Parameters:

Name | Type |
:------ | :------ |
`params` | [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams) |

**Returns:** *Promise*<[*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams)\>

Inherited from: [Transport](base_transport.transport.md)

Defined in: lib/lib/bcm2/src/base/transport.ts:109

___

### prepareRequest

▸ `Protected`**prepareRequest**(`params`: [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams)): *Promise*<[*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest)\>

Подготовка данных запроса

#### Parameters:

Name | Type |
:------ | :------ |
`params` | [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams) |

**Returns:** *Promise*<[*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest)\>

Overrides: [Transport](base_transport.transport.md)

Defined in: lib/lib/bcm2/src/http/transport.ts:426

___

### prepareResponse

▸ `Protected`**prepareResponse**(`request`: [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest), `rawResponse`: [*HttpTransportRawResponse*](../modules/http_transport_types.md#httptransportrawresponse), `params`: [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams)): *Promise*<[*HttpTransportResponse*](../modules/http_transport_types.md#httptransportresponse)\>

Подготовка ответа

#### Parameters:

Name | Type |
:------ | :------ |
`request` | [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest) |
`rawResponse` | [*HttpTransportRawResponse*](../modules/http_transport_types.md#httptransportrawresponse) |
`params` | [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams) |

**Returns:** *Promise*<[*HttpTransportResponse*](../modules/http_transport_types.md#httptransportresponse)\>

Overrides: [Transport](base_transport.transport.md)

Defined in: lib/lib/bcm2/src/http/transport.ts:505

___

### request

▸ `Protected`**request**(`request`: [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest)): *Promise*<[*HttpTransportRawResponse*](../modules/http_transport_types.md#httptransportrawresponse)\>

Отправка и обработка запроса (один раз без ретраев)

#### Parameters:

Name | Type |
:------ | :------ |
`request` | [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest) |

**Returns:** *Promise*<[*HttpTransportRawResponse*](../modules/http_transport_types.md#httptransportrawresponse)\>

Overrides: [Transport](base_transport.transport.md)

Defined in: lib/lib/bcm2/src/http/transport.ts:466

___

### retryAllowed

▸ `Protected`**retryAllowed**(`params`: [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams), `error`: Error): *boolean*

Проверка возможности ретраев запроса

#### Parameters:

Name | Type |
:------ | :------ |
`params` | [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams) |
`error` | Error |

**Returns:** *boolean*

Overrides: [Transport](base_transport.transport.md)

Defined in: lib/lib/bcm2/src/http/transport.ts:447

___

### send

▸ **send**(`params`: [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams)): *Promise*<[*HttpTransportResponse*](../modules/http_transport_types.md#httptransportresponse)\>

Отправка запроса

#### Parameters:

Name | Type |
:------ | :------ |
`params` | [*HttpTransportParams*](../modules/http_transport_types.md#httptransportparams) |

**Returns:** *Promise*<[*HttpTransportResponse*](../modules/http_transport_types.md#httptransportresponse)\>

Inherited from: [Transport](base_transport.transport.md)

Defined in: lib/lib/bcm2/src/base/transport.ts:218

___

### agent

▸ `Static`**agent**(`url`: *string*, `options`: [*HttpTransportAgentOptions*](../modules/http_transport_types.md#httptransportagentoptions)): [*HttpAgent*](../modules/http_transport_types.md#httpagent) \| [*HttpsAgent*](../modules/http_transport_types.md#httpsagent)

Получение инстанса агента для работы с запросом.

#### Parameters:

Name | Type |
:------ | :------ |
`url` | *string* |
`options` | [*HttpTransportAgentOptions*](../modules/http_transport_types.md#httptransportagentoptions) |

**Returns:** [*HttpAgent*](../modules/http_transport_types.md#httpagent) \| [*HttpsAgent*](../modules/http_transport_types.md#httpsagent)

Defined in: lib/lib/bcm2/src/http/transport.ts:579

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

Inherited from: [Transport](base_transport.transport.md)

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

Inherited from: [Transport](base_transport.transport.md)

Defined in: lib/lib/bcm2/src/base/model.ts:42

___

### prepareStream

▸ `Static` `Protected`**prepareStream**(`request`: [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest)): *Promise*<[*HttpTransportPreparedStream*](../modules/http_transport_types.md#httptransportpreparedstream)\> & { `cancel?`: () => *void*  }

Форматирование промиса для стримового запроса

#### Parameters:

Name | Type |
:------ | :------ |
`request` | [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest) |

**Returns:** *Promise*<[*HttpTransportPreparedStream*](../modules/http_transport_types.md#httptransportpreparedstream)\> & { `cancel?`: () => *void*  }

Defined in: lib/lib/bcm2/src/http/transport.ts:533

___

### setup

▸ `Static`**setup**<Current, Options\>(`options`: Options): [*ConcreteTransportClass*](../modules/base_transport.md#concretetransportclass)<Current, Options\>

#### Type parameters:

Name | Type |
:------ | :------ |
`Current` | [*AnyTransport*](../modules/base_transport.md#anytransport)<Options\> |
`Options` | [*HttpTransportOptions*](../modules/http_transport_types.md#httptransportoptions) |

#### Parameters:

Name | Type |
:------ | :------ |
`options` | Options |

**Returns:** [*ConcreteTransportClass*](../modules/base_transport.md#concretetransportclass)<Current, Options\>

Overrides: [Transport](base_transport.transport.md)

Defined in: lib/lib/bcm2/src/http/transport.ts:617
