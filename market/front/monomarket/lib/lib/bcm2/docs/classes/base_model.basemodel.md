[BCM2](../README.md) / [Exports](../modules.md) / [base/model](../modules/base_model.md) / BaseModel

# Class: BaseModel

[base/model](../modules/base_model.md).BaseModel

Базовый класс Моделей без мемоизации.

## Hierarchy

* **BaseModel**

  ↳ [*Backend*](base_backend.backend.md)

  ↳ [*Transport*](base_transport.transport.md)

## Table of contents

### Constructors

- [constructor](base_model.basemodel.md#constructor)

### Properties

- [context](base_model.basemodel.md#context)

### Methods

- [connect](base_model.basemodel.md#connect)
- [factory](base_model.basemodel.md#factory)

## Constructors

### constructor

\+ **new BaseModel**(`context`: [*Context*](base_context.context.md)): [*BaseModel*](base_model.basemodel.md)

#### Parameters:

Name | Type |
:------ | :------ |
`context` | [*Context*](base_context.context.md) |

**Returns:** [*BaseModel*](base_model.basemodel.md)

Defined in: lib/lib/bcm2/src/base/model.ts:26

## Properties

### context

• `Readonly` **context**: [*Context*](base_context.context.md)

Defined in: lib/lib/bcm2/src/base/model.ts:26

## Methods

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

Defined in: lib/lib/bcm2/src/base/model.ts:42
