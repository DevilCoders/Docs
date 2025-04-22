[BCM2](../README.md) / [Exports](../modules.md) / base/backend

# Module: base/backend

## Table of contents

### Classes

- [Backend](../classes/base_backend.backend.md)

### Type aliases

- [AnyBackend](base_backend.md#anybackend)
- [SetupBackend](base_backend.md#setupbackend)

## Type aliases

### AnyBackend

Ƭ **AnyBackend**<T, O\>: (...`args`: *any*[]) => [*Backend*](../classes/base_backend.backend.md)<InstanceType<T\>\>

#### Type parameters:

Name | Type |
:------ | :------ |
`T` | [*AnyTransport*](base_transport.md#anytransport)<O\> |
`O` | [*TransportOptions*](base_transport.md#transportoptions) |

#### Type declaration:

\+ (...`args`: *any*[]): [*Backend*](../classes/base_backend.backend.md)<InstanceType<T\>\>

#### Parameters:

Name | Type |
:------ | :------ |
`...args` | *any*[] |

**Returns:** [*Backend*](../classes/base_backend.backend.md)<InstanceType<T\>\>

Defined in: lib/lib/bcm2/src/base/backend.ts:25

___

### SetupBackend

Ƭ **SetupBackend**<B, T, O\>: (`context`: [*Context*](../classes/base_context.context.md)) => *BackendInstance*<B, T, O\> & (...`args`: *any*[]) => *BackendInstance*<B, T, O\> & B

#### Type parameters:

Name | Type |
:------ | :------ |
`B` | [*AnyBackend*](base_backend.md#anybackend)<T, O\> |
`T` | [*AnyTransport*](base_transport.md#anytransport)<O\> |
`O` | [*TransportOptions*](base_transport.md#transportoptions) |

Defined in: lib/lib/bcm2/src/base/backend.ts:20
