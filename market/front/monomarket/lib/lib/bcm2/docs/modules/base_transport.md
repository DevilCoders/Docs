[BCM2](../README.md) / [Exports](../modules.md) / base/transport

# Module: base/transport

## Table of contents

### Classes

- [Transport](../classes/base_transport.transport.md)

### Interfaces

- [TransportRawResponse](../interfaces/base_transport.transportrawresponse.md)
- [TransportRequest](../interfaces/base_transport.transportrequest.md)
- [TransportResponse](../interfaces/base_transport.transportresponse.md)
- [TransportStats](../interfaces/base_transport.transportstats.md)

### Type aliases

- [AnyTransport](base_transport.md#anytransport)
- [ConcreteTransportClass](base_transport.md#concretetransportclass)
- [ConcreteTransportInstance](base_transport.md#concretetransportinstance)
- [ExtractTransportOptions](base_transport.md#extracttransportoptions)
- [ExtractTransportOptionsC](base_transport.md#extracttransportoptionsc)
- [ExtractTransportParams](base_transport.md#extracttransportparams)
- [ExtractTransportResponse](base_transport.md#extracttransportresponse)
- [TransportOptions](base_transport.md#transportoptions)
- [TransportParams](base_transport.md#transportparams)

## Type aliases

### AnyTransport

Ƭ **AnyTransport**<O\>: (...`args`: *any*[]) => [*Transport*](../classes/base_transport.transport.md)<O\> & *any*

#### Type parameters:

Name | Type |
:------ | :------ |
`O` | [*TransportOptions*](base_transport.md#transportoptions) |

#### Type declaration:

\+ (...`args`: *any*[]): [*Transport*](../classes/base_transport.transport.md)<O\> & *any*

#### Parameters:

Name | Type |
:------ | :------ |
`...args` | *any*[] |

**Returns:** [*Transport*](../classes/base_transport.transport.md)<O\> & *any*

Defined in: lib/lib/bcm2/src/base/transport.ts:62

___

### ConcreteTransportClass

Ƭ **ConcreteTransportClass**<T, O\>: (`context`: [*Context*](../classes/base_context.context.md)) => [*ConcreteTransportInstance*](base_transport.md#concretetransportinstance)<T, O\> & (...`args`: *any*[]) => [*ConcreteTransportInstance*](base_transport.md#concretetransportinstance)<T, O\> & T

#### Type parameters:

Name | Type |
:------ | :------ |
`T` | [*AnyTransport*](base_transport.md#anytransport)<O\> |
`O` | [*TransportOptions*](base_transport.md#transportoptions) |

Defined in: lib/lib/bcm2/src/base/transport.ts:57

___

### ConcreteTransportInstance

Ƭ **ConcreteTransportInstance**<T, O\>: { `options`: O  } & *InstanceType*<T\>

#### Type parameters:

Name | Type |
:------ | :------ |
`T` | [*AnyTransport*](base_transport.md#anytransport)<O\> |
`O` | [*TransportOptions*](base_transport.md#transportoptions) |

Defined in: lib/lib/bcm2/src/base/transport.ts:54

___

### ExtractTransportOptions

Ƭ **ExtractTransportOptions**<T\>: [*TransportOptions*](base_transport.md#transportoptions) & T[*options*]

#### Type parameters:

Name | Type |
:------ | :------ |
`T` | [*Transport*](../classes/base_transport.transport.md) |

Defined in: lib/lib/bcm2/src/base/transport.ts:10

___

### ExtractTransportOptionsC

Ƭ **ExtractTransportOptionsC**<T\>: [*ExtractTransportOptions*](base_transport.md#extracttransportoptions)<InstanceType<T\>\>

#### Type parameters:

Name | Type |
:------ | :------ |
`T` | *typeof* [*Transport*](../classes/base_transport.transport.md) |

Defined in: lib/lib/bcm2/src/base/transport.ts:11

___

### ExtractTransportParams

Ƭ **ExtractTransportParams**<T\>: [*TransportParams*](base_transport.md#transportparams) & T[*send*] *extends* (`params`: *infer* Params) => *any* ? Params : *never*

#### Type parameters:

Name | Type |
:------ | :------ |
`T` | [*Transport*](../classes/base_transport.transport.md) |

Defined in: lib/lib/bcm2/src/base/transport.ts:16

___

### ExtractTransportResponse

Ƭ **ExtractTransportResponse**<T\>: [*TransportResponse*](../interfaces/base_transport.transportresponse.md) & T[*send*] *extends* (...`args`: *any*[]) => *Promise*<*infer* Response\> ? Response : *never*

#### Type parameters:

Name | Type |
:------ | :------ |
`T` | [*Transport*](../classes/base_transport.transport.md) |

Defined in: lib/lib/bcm2/src/base/transport.ts:13

___

### TransportOptions

Ƭ **TransportOptions**: *Partial*<{ [key: string]: *any*; `retry`: *number* ; `retryAllowed`: (`error`: Error) => *boolean* ; `retryDelay`: [*RetryDelay*](util_retry.md#retrydelay) \| *number*  }\>

Defined in: lib/lib/bcm2/src/base/transport.ts:19

___

### TransportParams

Ƭ **TransportParams**: *Partial*<{ [key: string]: *any*; `backend`: *string* ; `retry`: *number* ; `retryAllowed`: (`error`: Error) => *boolean* ; `retryDelay`: [*RetryDelay*](util_retry.md#retrydelay) \| *number*  }\>

Defined in: lib/lib/bcm2/src/base/transport.ts:26
