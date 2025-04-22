[BCM2](../README.md) / [Exports](../modules.md) / base/model

# Module: base/model

## Table of contents

### Classes

- [BaseModel](../classes/base_model.basemodel.md)

### Interfaces

- [Injection](../interfaces/base_model.injection.md)

### Type aliases

- [ConnectedClass](base_model.md#connectedclass)
- [ConnectedInstance](base_model.md#connectedinstance)

### Variables

- [Model](base_model.md#model)

## Type aliases

### ConnectedClass

Ƭ **ConnectedClass**<Class, InjectionDecl\>: (`context`: [*Context*](../classes/base_context.context.md)) => [*ConnectedInstance*](base_model.md#connectedinstance)<Class, InjectionDecl\> & (...`args`: *any*[]) => [*ConnectedInstance*](base_model.md#connectedinstance)<Class, InjectionDecl\> & Class

#### Type parameters:

Name | Type |
:------ | :------ |
`Class` | *typeof* [*BaseModel*](../classes/base_model.basemodel.md) |
`InjectionDecl` | [*Injection*](../interfaces/base_model.injection.md) |

Defined in: lib/lib/bcm2/src/base/model.ts:15

___

### ConnectedInstance

Ƭ **ConnectedInstance**<Class, InjectionDecl\>: *InstanceType*<Class\> & { readonly[Key in keyof InjectionDecl]: InstanceType<InjectionDecl[Key]\>}

#### Type parameters:

Name | Type |
:------ | :------ |
`Class` | *typeof* [*BaseModel*](../classes/base_model.basemodel.md) |
`InjectionDecl` | [*Injection*](../interfaces/base_model.injection.md) |

Defined in: lib/lib/bcm2/src/base/model.ts:11

## Variables

### Model

• `Const` **Model**: [*MemoedClass*](memo_memo_class.md#memoedclass)<*typeof* [*BaseModel*](../classes/base_model.basemodel.md)\>

Базовый класс Моделей с мемоизацией.

Defined in: lib/lib/bcm2/src/base/model.ts:99
