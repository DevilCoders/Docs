[BCM2](../README.md) / [Exports](../modules.md) / [base/client](../modules/base_client.md) / Client

# Class: Client

[base/client](../modules/base_client.md).Client

Базовый класс Клиента.

## Hierarchy

* [*Model*](../modules/base_model.md#model)

  ↳ **Client**

## Table of contents

### Constructors

- [constructor](base_client.client.md#constructor)

### Properties

- [context](base_client.client.md#context)

### Methods

- [connect](base_client.client.md#connect)
- [factory](base_client.client.md#factory)

## Constructors

### constructor

\+ **new Client**(`context`: [*Context*](base_context.context.md)): [*Client*](base_client.client.md)

#### Parameters:

Name | Type |
:------ | :------ |
`context` | [*Context*](base_context.context.md) |

**Returns:** [*Client*](base_client.client.md)

Inherited from: Model.constructor

Defined in: lib/lib/bcm2/src/base/model.ts:26

## Properties

### context

• `Readonly` **context**: [*Context*](base_context.context.md)

Inherited from: Model.context

Defined in: lib/lib/bcm2/src/base/model.ts:26

## Methods

### connect

▸ `Static`**connect**<Current, I, B\>(`injection`: *ClientInjection*<I, B\>): [*ConnectedClass*](../modules/base_model.md#connectedclass)<Current, ClientInjection<I, B\>\>

Настройка зависимостей и связи в бекендом

#### Type parameters:

Name | Type |
:------ | :------ |
`Current` | *typeof* [*Client*](base_client.client.md) |
`I` | [*Injection*](../interfaces/base_model.injection.md) |
`B` | [*AnyBackend*](../modules/base_backend.md#anybackend)<any, any\> |

#### Parameters:

Name | Type |
:------ | :------ |
`injection` | *ClientInjection*<I, B\> |

**Returns:** [*ConnectedClass*](../modules/base_model.md#connectedclass)<Current, ClientInjection<I, B\>\>

Overrides: Model.connect

Defined in: lib/lib/bcm2/src/base/client.ts:20

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

Inherited from: Model.factory

Defined in: lib/lib/bcm2/src/base/model.ts:42
